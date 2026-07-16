# The Sangam Route — Official Write-up

> **Warning:** This document contains the complete solution, archive password, and final flag.

## Challenge Information

**Challenge Name:** The Sangam Route

**Category:** Digital Forensics / OSINT / Miscellaneous

**Difficulty:** Medium

## Challenge Story

Dr. Yazhini Arul, an archaeologist researching ancient Tamil trade routes, has disappeared.

Investigators recovered a collection of files from her laptop, including photographs, travel tickets, browser history, expense records, a camera card image, and an encrypted archive.

At first, the evidence appears disconnected.

However, Yazhini's research was based on the five landscapes described in ancient Tamil Sangam literature:

- Kurinji
- Mullai
- Marutham
- Neithal
- Paalai

The participant must investigate the recovered digital evidence, identify the five landscapes, reconstruct Yazhini's true travel route, discover manipulated evidence, derive the password of the encrypted archive, and recover the final flag.

---

# 1. Initial Investigation

The first step is to inspect the challenge directory.

Run:

```bash
find challenge -type f | sort
```

The challenge contains the following files:

```text
challenge/archive/last_location.7z
challenge/browser/history.db
challenge/photos/camera_card.img
challenge/photos/IMG_1842.jpeg
challenge/photos/IMG_1931.jpeg
challenge/photos/research_backup.dat
challenge/photos/route_map.png
challenge/README.txt
challenge/records/expense_log.csv
challenge/research/reference_notes.txt
challenge/travel/bus_ticket_117.txt
challenge/travel/train_ticket_64.txt
```

Several different types of forensic evidence are present:

- JPEG images
- a suspicious DAT file
- a PNG image
- a disk image
- an SQLite database
- travel records
- expense records
- an encrypted 7-Zip archive

The goal is to determine how all these files are connected.

---

# 2. Read the Challenge Instructions

The participant should first inspect:

```bash
cat challenge/README.txt
```

The instructions introduce the disappearance of Dr. Yazhini and explain that her research focused on ancient Tamil landscapes.

The challenge suggests that the participant must reconstruct her journey using the available digital evidence.

---

# 3. Read the Landscape Reference Notes

The file:

```text
challenge/research/reference_notes.txt
```

contains information about the five Sangam landscapes.

Read it using:

```bash
cat challenge/research/reference_notes.txt
```

The reference information is:

```text
Kurinji
Mountain regions, waterfalls, mist, cold paths, hunters and flowering slopes.

Mullai
Forests, grazing lands, cattle, pastoral settlements and shaded paths.

Marutham
Agricultural plains, rivers, irrigation channels, fields and villages.

Neithal
Sea, coast, fishing boats, salt air, waves, ports and harbours.

Paalai
Dry roads, heat, thorn plants, scarce water and difficult journeys.
```

This information will be used to classify the recovered photographs.

---

# 4. Inspect the Photo Directory

List the files:

```bash
ls -lah challenge/photos
```

Then inspect their real file types:

```bash
file challenge/photos/*
```

The important discoveries are:

```text
IMG_1842.jpeg
JPEG image

IMG_1931.jpeg
JPEG image

research_backup.dat
JPEG image data

route_map.png
PNG image

camera_card.img
FAT32 filesystem image
```

This immediately reveals something suspicious.

The file:

```text
research_backup.dat
```

is not actually a DAT file.

It is a JPEG image disguised using a different file extension.

The camera card is also a filesystem image that may contain deleted data.

---

# 5. Recover the Mullai Landscape

The first visible image is:

```text
challenge/photos/IMG_1842.jpeg
```

Open the image:

```bash
xdg-open challenge/photos/IMG_1842.jpeg
```

The image represents a forest or pastoral landscape.

According to the reference notes:

```text
Mullai
Forests, grazing lands, cattle, pastoral settlements and shaded paths.
```

Therefore:

```text
IMG_1842.jpeg = Mullai
```

The corresponding challenge location is:

```text
Aamai Forest Camp
```

Therefore:

```text
IMG_1842.jpeg
↓
Mullai
↓
Aamai Forest Camp
```

---

# 6. Recover the Paalai Landscape

The second visible image is:

```text
challenge/photos/IMG_1931.jpeg
```

Open it:

```bash
xdg-open challenge/photos/IMG_1931.jpeg
```

The image represents a dry or arid environment.

According to the reference notes:

```text
Paalai
Dry roads, heat, thorn plants, scarce water and difficult journeys.
```

Therefore:

```text
IMG_1931.jpeg = Paalai
```

The corresponding challenge location is:

```text
Sembalai Crossing
```

Therefore:

```text
IMG_1931.jpeg
↓
Paalai
↓
Sembalai Crossing
```

---

# 7. Discover the Disguised Neithal Image

The file:

```text
challenge/photos/research_backup.dat
```

appears to be a data file.

However, running:

```bash
file challenge/photos/research_backup.dat
```

reveals:

```text
JPEG image data
```

This means the file extension is misleading.

Create a temporary JPEG copy:

```bash
cp challenge/photos/research_backup.dat recovered_neithal.jpeg
```

Open it:

```bash
xdg-open recovered_neithal.jpeg
```

The recovered photograph represents a coastal environment.

According to the reference notes:

```text
Neithal
Sea, coast, fishing boats, salt air, waves, ports and harbours.
```

Therefore:

```text
research_backup.dat = Neithal
```

The corresponding location is:

```text
Kadalpuram
```

Therefore:

```text
research_backup.dat
↓
Neithal
↓
Kadalpuram
```

The temporary recovered image can then be removed:

```bash
rm recovered_neithal.jpeg
```

---

# 8. Discover the Hidden Kurinji Image

The next suspicious file is:

```text
challenge/photos/route_map.png
```

At first, it appears to be an ordinary PNG image.

Inspect it using Binwalk:

```bash
binwalk challenge/photos/route_map.png
```

The output reveals:

```text
PNG image data

ZIP archive data

IMG_2120.jpeg
```

This proves that additional ZIP data has been appended to the PNG file.

The hidden archive contains:

```text
IMG_2120.jpeg
```

The participant can extract the embedded data using forensic tools.

After recovering and opening the image, it shows a mountainous landscape.

According to the reference notes:

```text
Kurinji
Mountain regions, waterfalls, mist, cold paths, hunters and flowering slopes.
```

Therefore:

```text
IMG_2120.jpeg = Kurinji
```

The corresponding location is:

```text
Velli Hills
```

Therefore:

```text
IMG_2120.jpeg
↓
Kurinji
↓
Velli Hills
```

---

# 9. Recover the Deleted Marutham Image

The final landscape image is not directly visible in the photo directory.

Inspect:

```text
challenge/photos/camera_card.img
```

Run:

```bash
file challenge/photos/camera_card.img
```

The output identifies it as a FAT32 filesystem image.

The filesystem appears empty.

However, deleted data may still exist inside the disk image.

Use PhotoRec:

```bash
photorec challenge/photos/camera_card.img
```

Inside PhotoRec:

1. Select the disk image.
2. Select the available partition.
3. Choose the filesystem type `Other`.
4. Search the whole filesystem.
5. Select a recovery destination outside the challenge directory.
6. Start the recovery process.

PhotoRec successfully recovers one JPEG image.

The recovered image represents agricultural land.

According to the reference notes:

```text
Marutham
Agricultural plains, rivers, irrigation channels, fields and villages.
```

Therefore:

```text
Recovered deleted JPEG = Marutham
```

The corresponding location is:

```text
Thenkarai Fields
```

Therefore:

```text
Deleted JPEG
↓
Marutham
↓
Thenkarai Fields
```

---

# 10. Complete Landscape Mapping

After the forensic investigation, all five landscapes have been recovered.

| Evidence | Landscape | Location |
|---|---|---|
| IMG_1842.jpeg | Mullai | Aamai Forest Camp |
| IMG_1931.jpeg | Paalai | Sembalai Crossing |
| research_backup.dat | Neithal | Kadalpuram |
| IMG_2120.jpeg | Kurinji | Velli Hills |
| Deleted JPEG from camera_card.img | Marutham | Thenkarai Fields |

However, identifying the landscapes is not enough.

The participant must determine the true order in which Yazhini visited them.

---

# 11. Analyze the EXIF Metadata

The next step is to inspect the photograph metadata.

Run:

```bash
exiftool challenge/photos/IMG_1842.jpeg
```

Then:

```bash
exiftool challenge/photos/IMG_1931.jpeg
```

Finally:

```bash
exiftool challenge/photos/research_backup.dat
```

The important timestamps are:

```text
IMG_1842.jpeg
Date/Time Original: 2026:01:14 07:20:00
```

```text
IMG_1931.jpeg
Date/Time Original: 2026:01:14 16:40:00
```

```text
research_backup.dat
Date/Time Original: 2026:01:16 14:30:00
```

At first, the timestamps suggest the following partial route:

```text
Mullai
↓
Paalai
↓
Neithal
```

However, the Neithal photograph appears to have been taken on January 16.

This conflicts with other evidence in the challenge.

The participant must therefore investigate additional sources before trusting the EXIF metadata.

---

# 12. Analyze the Expense Log

Read:

```bash
cat challenge/records/expense_log.csv
```

The expense records contain:

```text
date,time,item,location,amount

2026-01-14,07:10,breakfast,Aamai Forest Camp,65

2026-01-14,12:30,bus ticket,Aamai Forest Camp,145

2026-01-14,17:05,bottled water,Sembalai Crossing,30

2026-01-15,08:05,boat terminal tea,Kadalpuram,40

2026-01-15,14:45,train ticket,Kadalpuram,210

2026-01-15,18:20,guesthouse,Velli Hills,550

2026-01-16,08:40,field permit,Thenkarai Fields,100
```

Arrange the locations chronologically:

```text
Aamai Forest Camp
↓
Sembalai Crossing
↓
Kadalpuram
↓
Velli Hills
↓
Thenkarai Fields
```

Using the landscape mapping:

```text
Aamai Forest Camp = Mullai

Sembalai Crossing = Paalai

Kadalpuram = Neithal

Velli Hills = Kurinji

Thenkarai Fields = Marutham
```

Therefore, the expense log suggests the route:

```text
Mullai
↓
Paalai
↓
Neithal
↓
Kurinji
↓
Marutham
```

---

# 13. Analyze the Bus Ticket

Read:

```bash
cat challenge/travel/bus_ticket_117.txt
```

The ticket contains:

```text
SOUTHERN REGIONAL TRANSPORT

Passenger: Y. Arul
Date: 14-01-2026
Departure: 12:30

From: Aamai Forest Camp
To: Sembalai Crossing

Seat: 18
Ticket ID: SR117
```

This confirms:

```text
Aamai Forest Camp
↓
Sembalai Crossing
```

Using the landscape mapping:

```text
Mullai
↓
Paalai
```

The bus ticket therefore supports the expense log timeline.

---

# 14. Analyze the Train Ticket

Read:

```bash
cat challenge/travel/train_ticket_64.txt
```

The ticket contains:

```text
COASTAL HILL PASSENGER

Passenger: Y. Arul
Date: 15-01-2026
Departure: 14:45

From: Kadalpuram
To: Velli Hills

Coach: C2
Seat: 14
Ticket ID: CHP64
```

This confirms:

```text
Kadalpuram
↓
Velli Hills
```

Using the landscape mapping:

```text
Neithal
↓
Kurinji
```

Again, this supports the expense timeline.

---

# 15. Analyze the Browser History

The file:

```text
challenge/browser/history.db
```

is an SQLite database.

Query it directly:

```bash
sqlite3 challenge/browser/history.db \
"SELECT id, title, visit_time FROM urls ORDER BY visit_time;"
```

The output is:

```text
1|Sembalai Crossing afternoon weather|2026-01-14 09:10:00

2|Kadalpuram morning boat schedule|2026-01-14 19:35:00

3|Train from Kadalpuram to Velli Hills|2026-01-15 09:20:00

4|Thenkarai archaeological field permit|2026-01-15 20:05:00
```

The searches indicate Yazhini's intended journey.

She researched:

```text
Sembalai Crossing
↓
Kadalpuram
↓
Velli Hills
↓
Thenkarai Fields
```

This once again supports the route found in the expense log and travel records.

---

# 16. Identify the Manipulated Evidence

The EXIF timestamp of:

```text
research_backup.dat
```

claims:

```text
2026:01:16 14:30:00
```

However, the following independent evidence places Yazhini in Kadalpuram on January 15:

- the expense log
- the train ticket
- the browser history

Therefore, the EXIF metadata of the Neithal photograph is inconsistent with the rest of the evidence.

The correct conclusion is:

```text
The timestamp of research_backup.dat was manipulated.
```

The participant should not rely on a single source of forensic evidence.

The true route must be reconstructed by correlating multiple independent artifacts.

---

# 17. Determine the True Travel Route

After analyzing:

- landscape photographs
- EXIF metadata
- expense records
- travel tickets
- browser history

the true travel route is:

```text
Mullai
↓
Paalai
↓
Neithal
↓
Kurinji
↓
Marutham
```

Or:

```text
Mullai → Paalai → Neithal → Kurinji → Marutham
```

---

# 18. Read the Password Hint

Read:

```bash
cat challenge/field_notes/passwd_hint.txt
```

The hint states:

```text
The poems name the land.
The records reveal the journey.

Use the three-letter field abbreviations.
Arrange them in the true travel order.
Join them using hyphens.
```

The true route is:

```text
Mullai
Paalai
Neithal
Kurinji
Marutham
```

Take the first three letters:

```text
Mullai = MUL

Paalai = PAA

Neithal = NEI

Kurinji = KUR

Marutham = MAR
```

Arrange them in the true travel order:

```text
MUL
PAA
NEI
KUR
MAR
```

Join them using hyphens:

```text
MUL-PAA-NEI-KUR-MAR
```

Therefore, the archive password is:

```text
MUL-PAA-NEI-KUR-MAR
```

---

# 19. Test the Encrypted Archive

The final archive is:

```text
challenge/archive/last_location.7z
```

Test it using:

```bash
7z t challenge/archive/last_location.7z
```

Enter the password:

```text
MUL-PAA-NEI-KUR-MAR
```

The output should contain:

```text
Everything is Ok
```

This confirms that the reconstructed route and password are correct.

---

# 20. Extract the Final Archive

Extract the archive:

```bash
7z x challenge/archive/last_location.7z
```

Enter:

```text
MUL-PAA-NEI-KUR-MAR
```

The archive extracts:

```text
final_location.txt
```

Read it:

```bash
cat final_location.txt
```

The recovered document reveals the final location and flag.

---

# 21. Final Location

The investigation reveals Yazhini's final location:

```text
Kadalpuram Warehouse Marker 07
```

---

# 22. Final Flag

The final flag is:

```text
expX{kadalpuram_warehouse_07}
```

---

# Complete Solution Path

The intended solution chain is:

```text
Inspect challenge files
        ↓
Read Sangam landscape reference notes
        ↓
Classify IMG_1842.jpeg as Mullai
        ↓
Classify IMG_1931.jpeg as Paalai
        ↓
Detect research_backup.dat as a disguised JPEG
        ↓
Recover Neithal
        ↓
Analyze route_map.png with Binwalk
        ↓
Recover hidden IMG_2120.jpeg
        ↓
Identify Kurinji
        ↓
Analyze camera_card.img
        ↓
Recover deleted JPEG using PhotoRec
        ↓
Identify Marutham
        ↓
Analyze EXIF timestamps
        ↓
Analyze expense_log.csv
        ↓
Analyze bus and train tickets
        ↓
Query browser history.db
        ↓
Detect manipulated Neithal EXIF timestamp
        ↓
Reconstruct the true travel route
        ↓
Mullai → Paalai → Neithal → Kurinji → Marutham
        ↓
Generate archive password
        ↓
MUL-PAA-NEI-KUR-MAR
        ↓
Extract last_location.7z
        ↓
Recover final_location.txt
        ↓
expX{kadalpuram_warehouse_07}
```

---

# Tools Used

The challenge can be solved using the following tools:

```text
file
find
ls
cat
ExifTool
Binwalk
PhotoRec
SQLite3
7-Zip
```

---

# Flag

```text
expX{kadalpuram_warehouse_07}
```
