THE SANGAM ROUTE – MASTER PLAN

1. Challenge Information

Challenge Name:
The Sangam Route

Category:
Digital Forensics

Difficulty:
Medium

Primary Concepts:
- File signature analysis
- File carving
- Deleted file recovery
- Disk image analysis
- EXIF metadata analysis
- Timeline reconstruction
- SQLite database analysis
- Steganography / embedded archive discovery
- Evidence correlation
- Password reconstruction

---------------------------------------------------------------------------------

2. Story

Dr. Yazhini Arul, an archaeologist researching ancient Tamil trade routes,
has disappeared.

Her recovered laptop contains landscape photographs, travel records,
browser history, research notes, a camera card image, and a locked archive.

Investigators believe that Yazhini travelled through locations representing
the five landscapes described in ancient Sangam literature.

The participant must analyze the recovered evidence, reconstruct the true
travel route, determine the archive password, unlock the final archive,
and recover Yazhini's final field note.

Not every file is what it appears to be.

Not every timestamp can be trusted.

---------------------------------------------------------------------------------

3. Player Objective

The player must:

1. Investigate the recovered files.
2. Identify suspicious or disguised files.
3. Recover deleted evidence.
4. Analyze image metadata.
5. Examine travel records.
6. Investigate browser history.
7. Classify locations according to the five Sangam landscapes.
8. Reconstruct the true chronological journey.
9. Generate the archive password.
10. Unlock the encrypted archive.
11. Recover the final flag.

---------------------------------------------------------------------------------

4. True Travel Route

Mullai → Paalai → Neithal → Kurinji → Marutham

---------------------------------------------------------------------------------

5. Location Mapping

Mullai:
Aamai Forest Camp

Paalai:
Sembalai Crossing

Neithal:
Kadalpuram

Kurinji:
Velli Hills

Marutham:
Thenkarai Fields

---------------------------------------------------------------------------------

6. Sangam Landscape Classification

### Kurinji

Characteristics:

- Mountain regions
- Waterfalls
- Mist
- Cold paths
- Hunters
- Flowering slopes

Three-letter abbreviation:

KUR

---

### Mullai

Characteristics:

- Forests
- Grazing lands
- Cattle
- Pastoral settlements
- Shaded paths

Three-letter abbreviation:

MUL

---

### Marutham

Characteristics:

- Agricultural plains
- Rivers
- Irrigation channels
- Fields
- Villages

Three-letter abbreviation:

MAR

---

### Neithal

Characteristics:

- Sea
- Coast
- Fishing boats
- Salt air
- Waves
- Ports
- Harbours

Three-letter abbreviation:

NEI

---

### Paalai

Characteristics:

- Dry roads
- Heat
- Thorn plants
- Scarce water
- Difficult journeys

Three-letter abbreviation:

PAA

---------------------------------------------------------------------------------

7. Original Image Mapping

IMG_1842.jpeg:
Mullai

Location:
Aamai Forest Camp

Original fragment:
fragment_d.txt

---

IMG_1931.jpeg:
Paalai

Location:
Sembalai Crossing

Original fragment:
fragment_a.txt

---

IMG_2068.jpeg:
Neithal

Location:
Kadalpuram

Original fragment:
fragment_e.txt

---

IMG_2120.jpeg:
Kurinji

Location:
Velli Hills

Original fragment:
fragment_b.txt

---

IMG_2294.jpeg:
Marutham

Location:
Thenkarai Fields

Original fragment:
fragment_c.txt

---------------------------------------------------------------------------------

8. Final Player-Facing Photo Evidence

The player-facing photos directory contains:

camera_card.img

IMG_1842.jpeg

IMG_1931.jpeg

research_backup.dat

route_map.png

Not all files reveal their true purpose from their filename or extension.

---------------------------------------------------------------------------------

9. IMG_1842.jpeg

Classification:

Mullai

Location:

Aamai Forest Camp

EXIF Date/Time Original:

2026:01:14 07:20:00

Purpose:

Provides photographic and EXIF evidence for the beginning of the journey.

The participant should identify the landscape as Mullai using the
reference notes.

---------------------------------------------------------------------------------

10. IMG_1931.jpeg

Classification:

Paalai

Location:

Sembalai Crossing

EXIF Date/Time Original:

2026:01:14 16:40:00

Purpose:

Provides photographic and EXIF evidence for the second stage of the journey.

The participant should identify the landscape as Paalai.

---------------------------------------------------------------------------------

11. research_backup.dat

Actual File Type:

JPEG image

Classification:

Neithal

Location:

Kadalpuram

EXIF Date/Time Original:

2026:01:16 14:30:00

Purpose:

Introduces file signature analysis.

Although the extension is:

.dat

the file is actually a JPEG.

The participant can detect this using:

file

ExifTool

hex analysis

or similar forensic techniques.

The timestamp has been deliberately manipulated.

The purpose of this file is to introduce conflicting evidence into the
timeline.

The participant should eventually determine that the timestamp cannot
be trusted and use corroborating evidence from the expense log, browser
history, and travel records.

---------------------------------------------------------------------------------

12. camera_card.img

File Type:

FAT32 disk image

Size:

20 MB

Purpose:

Introduces deleted-file recovery and file carving.

The disk image originally contained:

IMG_2294.jpeg

Classification:

Marutham

Location:

Thenkarai Fields

The image was copied into the FAT32 disk image and subsequently deleted.

The participant must recover it using a forensic recovery technique.

Possible tools include:

PhotoRec

TestDisk

Autopsy

foremost

scalpel

or manual file carving.

Tested recovery method:

PhotoRec

The recovered image is renamed automatically by PhotoRec.

Example recovered filename:

f0000663.jpg

The participant must inspect the recovered image and classify it as
Marutham.

---------------------------------------------------------------------------------

13. route_map.png

File Type:

PNG image

Purpose:

Provides an additional forensic investigation path.

The participant should inspect the file rather than assuming it is only
an ordinary image.

Depending on the final challenge implementation, the file may contain
embedded or appended evidence.

The intended purpose is to encourage:

file inspection

metadata analysis

strings analysis

binwalk investigation

or archive extraction.

---------------------------------------------------------------------------------

14. Expense Timeline

File:

records/expense_log.csv

Contents:

2026-01-14 07:10
Breakfast
Aamai Forest Camp

2026-01-14 12:30
Bus ticket
Aamai Forest Camp

2026-01-14 17:05
Bottled water
Sembalai Crossing

2026-01-15 08:05
Boat terminal tea
Kadalpuram

2026-01-15 14:45
Train ticket
Kadalpuram

2026-01-15 18:20
Guesthouse
Velli Hills

2026-01-16 08:40
Field permit
Thenkarai Fields

Purpose:

Provides one of the strongest sources for reconstructing the actual
chronological journey.

---------------------------------------------------------------------------------

15. True Expense Timeline

2026-01-14 07:10

Aamai Forest Camp

Mullai

---

2026-01-14 17:05

Sembalai Crossing

Paalai

---

2026-01-15 08:05

Kadalpuram

Neithal

---

2026-01-15 18:20

Velli Hills

Kurinji

---

2026-01-16 08:40

Thenkarai Fields

Marutham

---------------------------------------------------------------------------------

16. Bus Ticket

File:

travel/bus_ticket_117.txt

Passenger:

Yazhini Arul

Date:

14-01-2026

Departure:

12:30

From:

Aamai Forest Camp

To:

Sembalai Crossing

Seat:

18

Ticket ID:

SR117

Purpose:

Confirms the movement:

Mullai → Paalai

---------------------------------------------------------------------------------

17. Train Ticket

File:

travel/train_ticket_64.txt

Passenger:

Yazhini Arul

Date:

15-01-2026

Departure:

14:45

From:

Kadalpuram

To:

Velli Hills

Coach:

C2

Seat:

14

Ticket ID:

CHP64

Purpose:

Confirms the movement:

Neithal → Kurinji

---------------------------------------------------------------------------------

18. Browser History Database

File:

browser/history.db

File Type:

SQLite database

Primary Table:

urls

Contents:

Sembalai Crossing afternoon weather

Visit Time:

2026-01-14 09:10:00

---

Kadalpuram morning boat schedule

Visit Time:

2026-01-14 19:35:00

---

Train from Kadalpuram to Velli Hills

Visit Time:

2026-01-15 09:20:00

---

Thenkarai archaeological field permit

Visit Time:

2026-01-15 20:05:00

Purpose:

Provides additional chronological evidence.

Participants should investigate the SQLite database using tools such as:

sqlite3

DB Browser for SQLite

Autopsy

or similar database analysis tools.

Example query:

SELECT id, title, visit_time FROM urls ORDER BY visit_time;

---------------------------------------------------------------------------------

19. Reference Notes

File:

research/reference_notes.txt

Purpose:

Explains the environmental characteristics of the five Sangam
landscapes.

The participant uses these descriptions to classify the recovered
photographs and locations.

The reference notes contain descriptions for:

Kurinji

Mullai

Marutham

Neithal

Paalai

---------------------------------------------------------------------------------

20. Password Hint

Original File:

field_notes/passwd_hint.txt

Original Hint:

The poems name the land.

The records reveal the journey.

Use the three-letter field abbreviations.

Arrange them in the true travel order.

Join them using hyphens.

Purpose:

Explains the password construction mechanism.

If the final version moves this clue into another forensic artifact,
such as the SQLite database, the plain text password hint should be
removed from the player-facing challenge.

---------------------------------------------------------------------------------

21. Timeline Conflict

The Neithal evidence stored as:

research_backup.dat

contains the EXIF timestamp:

2026:01:16 14:30:00

This timestamp is deliberately incorrect.

The true visit to Kadalpuram occurred on:

2026-01-15

Evidence supporting the true date includes:

expense_log.csv

train_ticket_64.txt

browser/history.db

The participant must recognize that EXIF metadata alone is insufficient
and reconstruct the timeline using multiple independent sources.

This is one of the primary forensic reasoning components of the
challenge.

---------------------------------------------------------------------------------

22. Archive

File:

archive/last_location.7z

Encryption:

7-Zip AES encryption

Header Encryption:

Enabled

Archive Contents:

final_location.txt

Purpose:

Final stage of the challenge.

The participant must reconstruct the journey and generate the correct
password.

---------------------------------------------------------------------------------

23. Password Construction

True Route:

Mullai → Paalai → Neithal → Kurinji → Marutham

Three-Letter Abbreviations:

Mullai:

MUL

Paalai:

PAA

Neithal:

NEI

Kurinji:

KUR

Marutham:

MAR

Join using hyphens.

Final Password:

MUL-PAA-NEI-KUR-MAR

---------------------------------------------------------------------------------

24. Final Location

Kadalpuram Warehouse Marker 07

---------------------------------------------------------------------------------

25. Final Flag

flag{kadalpuram_warehouse_07}

---------------------------------------------------------------------------------

26. Intended Solve Path

Stage 1:

Participant receives the challenge directory.

---

Stage 2:

Participant reads README.txt and understands that Dr. Yazhini Arul has
disappeared.

---

Stage 3:

Participant inventories the available files.

Possible commands:

find

ls

file

---

Stage 4:

Participant runs file signature analysis.

They discover:

research_backup.dat is actually a JPEG.

camera_card.img is a FAT32 filesystem image.

history.db is a SQLite database.

---

Stage 5:

Participant analyzes the visible photographs.

They use:

research/reference_notes.txt

to classify the landscapes.

---

Stage 6:

Participant analyzes EXIF metadata.

They discover timestamps associated with the photographs.

The Neithal photograph contains a suspicious timestamp.

---

Stage 7:

Participant investigates camera_card.img.

The disk image appears empty because the original image has been deleted.

---

Stage 8:

Participant performs deleted-file recovery.

Using PhotoRec or another forensic tool, they recover:

IMG_2294.jpeg

The recovered photograph represents:

Marutham

---

Stage 9:

Participant investigates:

records/expense_log.csv

This reveals chronological location evidence.

---

Stage 10:

Participant investigates the travel tickets.

The bus ticket confirms:

Aamai Forest Camp → Sembalai Crossing

The train ticket confirms:

Kadalpuram → Velli Hills

---

Stage 11:

Participant investigates:

browser/history.db

The SQLite browser history provides additional timeline evidence.

---

Stage 12:

Participant compares all timestamps.

They determine that the EXIF timestamp of:

research_backup.dat

is inconsistent with the remaining evidence.

---

Stage 13:

Participant reconstructs the true route:

Mullai → Paalai → Neithal → Kurinji → Marutham

---

Stage 14:

Participant applies the password construction rule.

MUL-PAA-NEI-KUR-MAR

---

Stage 15:

Participant extracts:

archive/last_location.7z

---

Stage 16:

Participant recovers:

final_location.txt

---

Stage 17:

Participant obtains the final flag:

flag{kadalpuram_warehouse_07}

---------------------------------------------------------------------------------

27. Tested Tools

The challenge has been tested using:

file

ExifTool

PhotoRec

mtools

sqlite3

7-Zip

find

grep

Standard Linux command-line utilities

---------------------------------------------------------------------------------

28. Tested PhotoRec Recovery

Test procedure:

1. Open camera_card.img using PhotoRec.

2. Select the detected filesystem.

3. Select:

Other

for FAT/NTFS/HFS+/ReiserFS filesystems.

4. Select a recovery destination outside the disk image.

5. Begin recovery.

Expected result:

One JPEG file recovered.

During testing, PhotoRec successfully recovered the deleted image.

----------------------------------------------------------------------------------

29. Player-Facing Directory Structure

challenge_files/

README.txt

archive/
    last_location.7z

browser/
    history.db

photos/
    camera_card.img
    IMG_1842.jpeg
    IMG_1931.jpeg
    research_backup.dat
    route_map.png

records/
    expense_log.csv

research/
    reference_notes.txt

travel/
    bus_ticket_117.txt
    train_ticket_64.txt

----------------------------------------------------------------------------------

30. Creator-Only Files

The following files must never be included in the player package:

MASTER_PLAN.md

solution files

original images

unencrypted final_location.txt

archive password documentation

final flag documentation

backup files

disk image construction files

PhotoRec recovery directories

creator scripts

----------------------------------------------------------------------------------

31. Pre-Release Verification

Before releasing the challenge:

1. Verify final_location.txt is not outside the encrypted archive.

2. Verify no original image backups exist in challenge_files.

3. Verify no PhotoRec recovery directories exist in challenge_files.

4. Verify the archive password works.

5. Verify the deleted JPEG can be recovered from camera_card.img.

6. Verify research_backup.dat is detected as JPEG.

7. Verify EXIF timestamps are present.

8. Verify history.db opens correctly.

9. Verify expense_log.csv contains the intended timeline.

10. Verify both travel tickets contain the intended evidence.

11. Verify README.txt contains no solution spoilers.

12. Search for accidental flag exposure.

Recommended command:

grep -RniE 'flag\{|MUL-PAA-NEI-KUR-MAR|kadalpuram_warehouse_07' challenge_files/

Expected result:

No plaintext solution exposure.

----------------------------------------------------------------------------------

32. Challenge Design Philosophy

The Sangam Route is designed as a multi-artifact digital forensics
investigation.

No single piece of evidence should reveal the entire solution.

Participants must correlate:

file signatures

deleted files

photographs

EXIF metadata

expense records

travel tickets

browser history

Sangam landscape classifications

and encrypted archives.

The central forensic lesson is:

A single timestamp should not automatically be trusted.

Reliable conclusions require correlation between multiple independent
sources of evidence.
