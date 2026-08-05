# 12 — Metadata OSINT

## My Approach

Metadata is one of those things people usually ignore.

A file can look completely normal when you open it, but the file itself may contain extra information about how it was created, edited, exported, or processed.

For OSINT, I use metadata as a **supporting clue**.

I never treat one metadata field as proof of identity.

My basic flow is:

**Public File → Extract Metadata → Find Interesting Clues → Correlate → Verify → Document**

---

# 1. What Is Metadata?

Metadata is information stored inside or associated with a file.

Depending on the file type, it can include:

* File name
* File type
* Creation time
* Modification time
* Author
* Creator
* Software
* Device
* Camera model
* GPS coordinates
* Copyright
* Description
* Comments
* Document title
* PDF producer
* Editing software

Not every file contains all of these.

---

# 2. My First Rule

I don't immediately look for someone's location or identity.

First I ask:

**What metadata actually exists in this file?**

Then I decide whether any of it creates a useful OSINT pivot.

---

# 3. Install the Basic Tools

On Kali:

```bash
sudo apt update
sudo apt install exiftool poppler-utils mediainfo file
```

Check:

```bash
exiftool -ver
pdfinfo -v
mediainfo --Version
file --version
```

These cover most of my basic metadata work.

---

# 4. Start With `file`

Before using specialized tools, I check what the file actually is:

```bash
file image.jpg
```

Example:

```text
image.jpg: JPEG image data
```

For a document:

```bash
file report.pdf
```

This prevents me from assuming the extension tells the whole story.

---

# 5. ExifTool

My main metadata tool is:

```bash
exiftool image.jpg
```

It can display many fields depending on the file.

For example:

```text
File Name
File Size
File Type
Image Width
Image Height
Create Date
Modify Date
Camera Make
Camera Model
GPS Position
Software
```

I don't expect every image to contain these fields.

---

# 6. Image Metadata

For a publicly available image:

```bash
exiftool photo.jpg
```

I pay attention to:

```text
Make
Model
Date/Time
Software
GPS
Copyright
Description
Comment
```

The interesting part is not simply finding metadata.

The interesting part is determining whether the metadata gives me a **new, verifiable pivot**.

---

# 7. Camera Information

Suppose I find:

```text
Make: Example
Model: Example Phone
```

This tells me something about the device used to create the file.

But it doesn't prove:

**The target owns this phone.**

Someone could have:

* Borrowed the device
* Received the image
* Edited the file
* Re-exported the image
* Changed metadata

So I treat it as supporting evidence only.

---

# 8. GPS Metadata

GPS is one of the most sensitive metadata fields.

I can check:

```bash
exiftool photo.jpg | grep -i gps
```

If coordinates exist, ExifTool may display:

```text
GPS Latitude
GPS Longitude
GPS Position
```

I record the information carefully.

I don't publish someone's exact private location simply because metadata exposed it.

---

# 9. GPS Is Not Always Current

Even if a photo contains GPS coordinates, it only tells me where the file was geotagged.

It doesn't necessarily mean:

* The person currently lives there
* The person was there recently
* The photo was taken by the target
* The file hasn't been edited

Context matters.

---

# 10. Convert Coordinates

If I have legitimate public coordinates and need to understand the location, I can convert them into a map location.

For example:

```text
33.6844, 73.0479
```

But I distinguish between:

**Photo coordinate**

and

**Person's location**

Those are not automatically the same thing.

---

# 11. Metadata From Multiple Images

One image can be misleading.

If I have several public images:

```text
photo1.jpg
photo2.jpg
photo3.jpg
```

I compare them:

```bash
exiftool photo1.jpg
exiftool photo2.jpg
exiftool photo3.jpg
```

I look for repeated information such as:

* Same camera model
* Similar software
* Similar timestamps
* Similar metadata structure

Repeated patterns can increase confidence, but still aren't identity proof.

---

# 12. Batch Metadata

For multiple files:

```bash
exiftool *.jpg
```

Or:

```bash
exiftool -csv *.jpg > metadata.csv
```

Now I can open the metadata in a spreadsheet and compare files.

This is much easier when dealing with many public files.

---

# 13. PDF Metadata

For a PDF:

```bash
exiftool report.pdf
```

I can also use:

```bash
pdfinfo report.pdf
```

Important fields may include:

```text
Title
Author
Creator
Producer
CreationDate
ModDate
Pages
```

For example:

```text
Author: Fawad Qureshi
Creator: Microsoft Word
Producer: Adobe PDF
```

This is a clue.

It is not automatic proof that the named person created the document.

---

# 14. PDF Author

If I find:

```text
Author: Example Name
```

I search the name independently:

```text
"Example Name"
```

Then compare it with:

* Organization
* Project
* Website
* Public profile
* Publication
* Event

If several independent sources agree, confidence increases.

---

# 15. PDF Creation Date

I check:

```text
CreationDate
ModDate
```

This can help build a timeline.

Example:

```text
Document created:
2024

Project announced:
2024

Public website appeared:
2025
```

These dates can help establish chronology.

But file timestamps can change when a document is copied, edited or exported.

---

# 16. Office Documents

Public DOCX/XLSX/PPTX files can contain metadata too.

For example:

```bash
exiftool presentation.pptx
```

I may find:

```text
Author
Last Modified By
Created
Modified
Application
Company
```

Again, I treat these as clues.

---

# 17. `Last Modified By`

This field can be interesting.

Example:

```text
Last Modified By:
Example Name
```

I don't immediately attribute the entire document to that person.

The field may represent:

* The last editor
* A template owner
* A computer account
* A previous user
* Automatically inherited information

I verify independently.

---

# 18. Software Information

Metadata may show:

```text
Software:
Adobe Photoshop
```

or:

```text
Creator:
Microsoft PowerPoint
```

This can tell me how a file was processed.

It can also help distinguish:

```text
Original camera file
```

from:

```text
Edited/exported file
```

---

# 19. Image Editing Clues

Suppose an image says:

```text
Software:
Adobe Photoshop
```

That suggests the file was processed by Photoshop.

It does **not** prove the image was fake.

It may simply have been:

* Cropped
* Resized
* Compressed
* Annotated
* Color corrected

Metadata tells me something happened to the file, not necessarily what happened.

---

# 20. Social Media Changes Everything

This is extremely important.

Platforms often process uploaded media.

They may:

* Recompress images
* Resize images
* Remove metadata
* Re-encode videos
* Strip GPS information

Therefore:

**No metadata ≠ no information about the original file.**

It simply means the copy I obtained may no longer contain the original metadata.

---

# 21. Compare Original vs Reprocessed Files

If I have two publicly available versions:

```text
Original.pdf
Downloaded-copy.pdf
```

or:

```text
original.jpg
social-media-copy.jpg
```

I compare their metadata.

This can tell me whether one version has been reprocessed.

I don't assume the metadata difference means the content itself is different.

---

# 22. File Names

File names themselves can become clues.

Examples:

```text
Fawad_Project_Final.pdf
presentation_final2.pptx
conference_2025.pdf
IMG_20240721_123456.jpg
```

I don't treat the filename as proof.

But it can provide:

* Project name
* Event
* Date
* Internal naming pattern
* Potential username

A filename can become another search pivot.

---

# 23. Search a Unique Filename

If I find:

```text
cybersecurity_project_final.pdf
```

I search:

```text
"cybersecurity_project_final.pdf"
```

This may reveal:

* Copies
* Older versions
* References
* Original publisher
* Other public locations

---

# 24. Comments and Descriptions

Some files contain:

```text
Comment
Description
Subject
Keywords
```

I check:

```bash
exiftool file.pdf | grep -Ei "comment|description|subject|keyword"
```

Sometimes these fields contain useful context.

Sometimes they are completely empty.

---

# 25. Embedded Thumbnails

Some image files can contain embedded thumbnails.

I inspect the file using:

```bash
exiftool image.jpg
```

and, where appropriate, extract embedded previews with ExifTool.

I don't assume the thumbnail represents a different original image.

It may simply be an automatically generated preview.

---

# 26. Video Metadata

For videos:

```bash
exiftool video.mp4
```

and:

```bash
mediainfo video.mp4
```

I can inspect:

* Duration
* Resolution
* Codec
* Frame rate
* Creation time
* Encoder
* Audio information
* Software

Example:

```text
Duration:
00:01:32

Width:
1920

Height:
1080

Frame rate:
30 FPS
```

These are technical clues, not identity proof.

---

# 27. Audio Metadata

For public audio:

```bash
exiftool audio.mp3
```

or:

```bash
mediainfo audio.mp3
```

Possible fields:

* Artist
* Album
* Title
* Encoder
* Software
* Date
* Copyright

Again, I verify the information independently.

---

# 28. `strings`

Sometimes I inspect printable text:

```bash
strings file.jpg | less
```

Or:

```bash
strings document.pdf | grep -i "http"
```

This can reveal embedded URLs or other readable strings.

It is not a replacement for proper metadata tools.

It's simply another inspection method.

---

# 29. Metadata + Username

Suppose I find a public image associated with:

```text
@redteamerx
```

Metadata shows:

```text
Software:
Example Software
```

I don't say:

**This proves @redteamerx uses this software.**

Instead:

```text
Public image
↓
Metadata
↓
Software information
↓
Compare with other public files
↓
Independent verification
```

That is the correct way to handle it.

---

# 30. Metadata + Public Documents

Suppose I find:

```text
Public PDF
↓
Author: Example Name
↓
Project: Example Project
```

I search:

```text
"Example Name" "Example Project"
```

If the same combination appears on an official website, confidence becomes stronger.

---

# 31. Metadata + Timeline

I can combine:

```text
File metadata
↓
Creation date
↓
Public post date
↓
Project announcement
↓
Website history
```

This can help establish a timeline.

I don't use timestamps alone to establish identity.

---

# 32. Metadata + Other OSINT

My strongest results usually come from combining multiple sources.

Example:

```text
Public image
↓
Metadata
↓
Camera information

Public profile
↓
Same person

Public document
↓
Same project

Public website
↓
Same organization
```

Now I have multiple independent clues.

That's much stronger than one metadata field.

---

# 33. Check Whether Metadata Is Trustworthy

Before using a metadata finding, I ask:

1. Was this the original file?
2. Could the platform have modified it?
3. Could the metadata have been manually changed?
4. Is the timestamp reasonable?
5. Does another source support it?
6. Does the metadata actually relate to the target?

If the answer is unclear, I mark the finding as uncertain.

---

# 34. My Confidence Model

### Low

One metadata field.

Example:

```text
Author: Fawad
```

### Medium

Metadata + another public source.

Example:

```text
Author: Fawad
+
same project appears on public profile
```

### High

Metadata + multiple independent public sources + consistent timeline.

The confidence comes from **correlation**, not simply from having more metadata fields.

---

# 35. Preserve the Original File

I keep the downloaded public file unchanged:

```text
original/
    photo.jpg
```

Then analysis separately:

```text
analysis/
    metadata.txt
```

I can export metadata:

```bash
exiftool photo.jpg > metadata.txt
```

This makes the investigation reproducible.

---

# 36. Hash the File

I can calculate:

```bash
sha256sum photo.jpg
```

This gives me a fingerprint of the exact file I analyzed.

If I later download another copy, I can compare hashes.

---

# 37. Metadata Collection Record

For each file:

```text
File:
photo.jpg

Source:
Public URL

Collected:
YYYY-MM-DD

File hash:
SHA-256

Metadata found:
Camera model
Software
Date

GPS:
Present / Not present

Interesting clue:
...

Independent confirmation:
...

Confidence:
Low / Medium / High
```

This keeps my findings organized.

---

# 38. Things I Never Assume

I never assume:

```text
Author = Owner
```

or:

```text
GPS = Current Location
```

or:

```text
Camera = Person
```

or:

```text
Timestamp = Exact Event Time
```

or:

```text
Filename = Creator
```

These can all be misleading without context.

---

# 39. Common Metadata Mistakes

### Mistake 1

Finding a GPS coordinate and immediately publishing it.

Bad practice.

### Mistake 2

Treating an author field as identity proof.

Wrong.

### Mistake 3

Assuming missing metadata means the file has no useful information.

Wrong.

### Mistake 4

Ignoring platform processing.

Very common mistake.

### Mistake 5

Using a timestamp without checking timezone or file history.

Wrong.

### Mistake 6

Trusting metadata that conflicts with every other source.

Investigate the conflict instead.

---

# 40. My Practical Workflow

```text
Public File
↓
Identify File Type
↓
Preserve Original
↓
Calculate SHA-256
↓
Run ExifTool
↓
Run File-Specific Tool
↓
Extract Interesting Metadata
↓
Check Dates
↓
Check Software / Device
↓
Check GPS if legitimately present
↓
Compare With Other Files
↓
Search New Identifiers
↓
Correlate With Public Sources
↓
Verify
↓
Document
```

---

# 41. My Point of View

Metadata is powerful because it can give context that isn't immediately visible.

A normal-looking file might contain:

```text
Author
↓
Software
↓
Device
↓
Date
↓
Location
↓
Project
```

But the important part isn't finding the metadata.

The important part is **knowing what the metadata actually proves**.

If I find:

```text
GPS: Islamabad
```

I don't write:

**The target lives in Islamabad.**

I write something closer to:

**The analyzed public file contained metadata indicating Islamabad coordinates. This does not independently establish the target's residence or current location.**

That difference is what separates proper OSINT from guessing.

---

# Final Rule

**Metadata is evidence of file properties, not automatic evidence of a person's identity.**

Extract it.

Understand it.

Correlate it.

Verify it.

And be careful with sensitive information such as exact GPS coordinates.

**File → Metadata → Clue → Correlation → Verification → Intelligence**
