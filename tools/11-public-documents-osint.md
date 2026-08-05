# 11 — Public Documents OSINT

## My Approach

Public documents are one of my favorite OSINT pivots because people often publish useful information without realizing how many other clues are sitting inside the same document.

I don't start by trying to find private files.

I start with documents that are **already publicly accessible** through search engines, websites, repositories, universities, companies, conferences, government portals, blogs or other public sources.

My basic flow is:

**Identifier → Search → Public Document → Extract Clues → Correlate → Verify → Document**

---

# 1. Start With the Target Identifier

If I have a public name:

```text
"Fawad Qureshi"
```

I can search for public documents:

```text
"Fawad Qureshi" filetype:pdf
```

Then:

```text
"Fawad Qureshi" filetype:doc
```

```text
"Fawad Qureshi" filetype:ppt
```

```text
"Fawad Qureshi" filetype:xls
```

I don't assume every result belongs to my target.

The document itself has to provide enough context.

---

# 2. Search by Username

If the only identifier I have is a username:

```text
"redteamerx" filetype:pdf
```

Then:

```text
"redteamerx" filetype:ppt
```

And:

```text
"redteamerx" filetype:doc
```

A username appearing inside a document is a lead.

I still verify whether it is the same person.

---

# 3. Search by Organization

If I discover an organization:

```text
"Example Organization" filetype:pdf
```

I can find public:

* Reports
* Presentations
* Research papers
* Event material
* Brochures
* Public notices
* Technical documentation

Then I search inside those documents for useful identifiers.

---

# 4. Search by Project

A project name can become another pivot.

For example:

```text
"BlackTrace" filetype:pdf
```

Then:

```text
"BlackTrace" filetype:ppt
```

And:

```text
"BlackTrace" "Fawad Qureshi" filetype:pdf
```

A project can connect:

**Person → Project → Organization → Document → Website**

---

# 5. Useful File Types

I normally look for:

```text
PDF
DOC
DOCX
PPT
PPTX
XLS
XLSX
CSV
TXT
```

PDF is particularly useful because public reports and presentations are commonly published in that format.

---

# 6. Use `site:`

If I know the organization's website:

```text
site:example.com filetype:pdf
```

Then:

```text
site:example.com "Fawad Qureshi" filetype:pdf
```

Or:

```text
site:example.com cybersecurity filetype:pdf
```

This reduces irrelevant search results.

---

# 7. Search Specific Words

Sometimes I don't know the document title.

I search combinations such as:

```text
"Fawad Qureshi" presentation filetype:pdf
```

```text
"Fawad Qureshi" research filetype:pdf
```

```text
"Fawad Qureshi" conference filetype:ppt
```

```text
"Fawad Qureshi" project filetype:pdf
```

The idea is to combine an identifier with context.

---

# 8. Search Exact Document Titles

If I find:

```text
Annual Cybersecurity Report 2025
```

I search the exact title:

```text
"Annual Cybersecurity Report 2025"
```

Then:

```text
"Annual Cybersecurity Report 2025" pdf
```

This can reveal:

* Original source
* Copies
* Older versions
* References
* News articles
* Other organizations mentioning it

---

# 9. Find the Original Source

This is important.

I may find the same PDF on multiple websites.

For example:

```text
Website A
↓
PDF

Website B
↓
Same PDF

Website C
↓
Same PDF
```

I don't automatically treat all three as separate evidence.

I try to locate the original publisher.

The original source is usually stronger evidence than a random mirror.

---

# 10. Download Public Documents

If the document is legitimately public, I can download it for analysis.

Example:

```bash
wget "https://example.com/report.pdf" -O report.pdf
```

Or:

```bash
curl -L "https://example.com/report.pdf" -o report.pdf
```

I keep the original file unchanged.

This is useful because I may need to inspect its metadata later.

---

# 11. Check Basic PDF Information

On Kali:

```bash
pdfinfo report.pdf
```

This can show information such as:

* Title
* Author
* Creator
* Producer
* Creation date
* Modification date
* Number of pages
* PDF version

Example:

```text
Title:
Author:
Creator:
Producer:
CreationDate:
ModDate:
Pages:
```

I treat these fields as clues.

---

# 12. Use ExifTool

Another useful tool:

```bash
exiftool report.pdf
```

It may provide additional metadata depending on the file.

For example:

```bash
exiftool report.pdf | less
```

Then I look for:

```text
Author
Creator
Producer
Create Date
Modify Date
Title
Subject
```

Metadata can be extremely useful, but it can also be missing, changed or automatically generated.

---

# 13. Metadata Is Not Identity Proof

Suppose I find:

```text
Author: Fawad Qureshi
```

I don't immediately conclude:

**This proves the target created the document.**

The metadata may have been:

* Manually entered
* Inherited from a template
* Copied from another document
* Automatically generated
* Modified later

I need additional evidence.

---

# 14. Extract PDF Text

I can use:

```bash
pdftotext report.pdf report.txt
```

Then:

```bash
cat report.txt
```

Or:

```bash
less report.txt
```

Now I can search the document much faster.

---

# 15. Search Inside the Extracted Text

For example:

```bash
grep -in "Fawad" report.txt
```

Search for email:

```bash
grep -Ein "email|@" report.txt
```

Search for websites:

```bash
grep -Ein "https?://|www\." report.txt
```

Search for organization names:

```bash
grep -in "organization" report.txt
```

This is much faster than manually reading a 100-page document.

---

# 16. Extract URLs

A document may contain links that aren't immediately obvious.

After converting it to text:

```bash
grep -Eo 'https?://[^ ]+' report.txt
```

I then investigate the publicly referenced URLs.

For example:

```text
PDF
↓
Website
↓
Project
↓
GitHub
```

One document can create several new pivots.

---

# 17. Search for Public Email Addresses

If the document contains an email address:

```bash
grep -Eio '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}' report.txt
```

I record the address if it is relevant and publicly published.

I don't use it to access accounts.

It is simply another public identifier.

---

# 18. Search for Names

I look for:

* Authors
* Contributors
* Speakers
* Researchers
* Editors
* Project members

For example:

```text
Author:
Fawad Qureshi
```

Then I compare that name against other public sources.

---

# 19. Search for Dates

Dates are useful for building timelines.

I record things such as:

```text
Publication date
Event date
Report date
Creation date
Modification date
Project date
```

Then I compare them with information from:

* Social media
* Websites
* GitHub
* News
* Events
* Archived pages

---

# 20. Search for Organizations

A document may mention:

```text
Company
University
Conference
Research group
Project
Department
```

Each one can become another pivot.

Example:

```text
Person
↓
Public document
↓
University
↓
University website
↓
Public profile
```

---

# 21. Search for Locations

Public documents can mention:

* City
* Country
* Campus
* Office
* Event venue
* Conference location

I treat location information carefully.

A location in a document may describe an event rather than the person's current location.

Context matters.

---

# 22. Search for Public Profiles

If a document contains:

```text
linkedin.com/...
github.com/...
x.com/...
instagram.com/...
```

I follow those publicly available links.

I then compare:

* Name
* Username
* Organization
* Project
* Profile image
* Dates

Multiple matching identifiers make the connection stronger.

---

# 23. Search for Document Copies

Sometimes a document disappears from its original website but remains publicly available elsewhere.

I search the exact title:

```text
"Document Title"
```

And distinctive phrases:

```text
"unique sentence from the document"
```

This can reveal copies or references.

I record the date and source of each version.

---

# 24. Search Distinctive Phrases

A unique sentence can be a very strong search pivot.

For example:

```text
"unique phrase from this report"
```

Then I check where that phrase appears elsewhere.

This can reveal:

* Older versions
* Conference copies
* Blog posts
* Reposts
* Related projects

It can also reveal plagiarism or duplicated material.

---

# 25. Compare Document Versions

Suppose I find:

```text
report-2023.pdf
report-2024.pdf
report-2025.pdf
```

I compare:

* Authors
* Dates
* Organizations
* Project names
* Links
* Contact information
* Technical references

Changes between versions can provide useful historical context.

---

# 26. OCR for Scanned Documents

Some PDFs contain images instead of selectable text.

If normal extraction gives nothing:

```bash
pdftotext scanned.pdf output.txt
```

and the output is empty or incomplete, I consider OCR.

A common tool is:

```bash
ocrmypdf
```

For example:

```bash
ocrmypdf scanned.pdf searchable.pdf
```

Then:

```bash
pdftotext searchable.pdf output.txt
```

Now the scanned document can be searched as text.

Only use OCR on documents that are legitimately accessible.

---

# 27. Strings

Sometimes useful information exists inside a file even when it isn't visible normally.

I can inspect printable strings:

```bash
strings report.pdf | less
```

Then search:

```bash
strings report.pdf | grep -i "http"
```

This isn't magic.

It simply exposes printable text embedded in the file.

---

# 28. Document Links

PDFs can contain clickable links.

Depending on the document, I may inspect them with PDF analysis tools or extract them manually.

A link might lead to:

```text
PDF
↓
Website
↓
GitHub
↓
Project
```

That new URL becomes another OSINT pivot.

---

# 29. Public Presentations

Presentations can be especially useful.

Search:

```text
"Fawad Qureshi" presentation
```

```text
"Fawad Qureshi" filetype:pptx
```

```text
"Fawad Qureshi" conference filetype:pdf
```

Presentations may contain:

* Speaker name
* Organization
* Project names
* Event
* Date
* Public social links
* Technical topics

I verify the event and source before attributing the presentation.

---

# 30. Public University Documents

University websites can contain public:

* Research papers
* Event programs
* Student projects
* Conference material
* Department reports
* Public presentations

I can search:

```text
site:university.edu "Fawad Qureshi" filetype:pdf
```

The same principle applies to other public institutions.

---

# 31. Public Company Documents

Companies may publish:

* Reports
* Whitepapers
* Technical documentation
* Press releases
* Presentations
* Security advisories

For example:

```text
site:example.com filetype:pdf
```

Then:

```text
site:example.com "Fawad Qureshi" filetype:pdf
```

---

# 32. Public Technical Reports

Technical documents can reveal:

* Product names
* Technologies
* Domains
* Project names
* Developers
* Public repositories
* Architecture descriptions

I use these as pivots.

I don't treat technical details as permission to attack the infrastructure.

---

# 33. Document → Metadata → Search

A useful chain is:

```text
Public PDF
↓
Metadata
↓
Author
↓
Search author
↓
Public profile
↓
Organization
```

But I always verify the connection independently.

---

# 34. Document → URL → Domain

Another useful chain:

```text
Public PDF
↓
Embedded URL
↓
Domain
↓
DNS
↓
Certificates
↓
Public website
```

Now the document has connected to the technical footprint.

---

# 35. Document → Project → GitHub

For technical reports:

```text
Document
↓
Project name
↓
Search GitHub
↓
Public repository
↓
Contributor
```

Again, a contributor name is a lead.

It isn't automatically proof that every similarly named person is the same target.

---

# 36. Search Engine Queries I Use

Basic:

```text
"Fawad Qureshi" filetype:pdf
```

Username:

```text
"redteamerx" filetype:pdf
```

Organization:

```text
"Organization Name" filetype:pdf
```

Project:

```text
"Project Name" filetype:pdf
```

Specific website:

```text
site:example.com filetype:pdf
```

Specific context:

```text
"Fawad Qureshi" cybersecurity filetype:pdf
```

Presentation:

```text
"Fawad Qureshi" filetype:pptx
```

---

# 37. My Basic Toolset

For public document analysis I commonly use:

### Search

```text
Google
Bing
```

### Metadata

```bash
exiftool
pdfinfo
```

### PDF text

```bash
pdftotext
```

### File inspection

```bash
strings
file
```

### OCR

```text
OCRmyPDF
Tesseract
```

### Basic command-line processing

```bash
grep
sed
awk
sort
uniq
```

I don't need every tool for every document.

---

# 38. Install Basic Tools on Kali

```bash
sudo apt update
sudo apt install exiftool poppler-utils file binutils grep
```

For OCR:

```bash
sudo apt install ocrmypdf tesseract-ocr
```

Check:

```bash
exiftool -ver
pdfinfo -v
pdftotext -v
tesseract --version
```

---

# 39. My Practical Workflow

```text
Target
↓
Name / Username / Organization / Project
↓
Search public documents
↓
Find original source
↓
Download public document
↓
Hash / preserve original
↓
Check metadata
↓
Extract text
↓
Extract URLs
↓
Extract names
↓
Extract public identifiers
↓
Search new identifiers
↓
Correlate with other sources
↓
Verify
↓
Document
```

---

# 40. Preserve the Original

When I download a document for research, I don't immediately modify it.

I keep the original:

```text
original/
    report.pdf
```

Then I create extracted files separately:

```text
analysis/
    report.txt
    metadata.txt
```

This keeps my evidence organized.

---

# 41. Hash the File

For documentation, I can calculate a hash:

```bash
sha256sum report.pdf
```

Example:

```text
SHA256:
[hash]
```

This allows me to identify the exact file I analyzed.

If the public document changes later, I can tell that I was working with a different version.

---

# 42. Evidence Notes

For each document I record:

```text
Document:
report.pdf

Source:
https://example.com/report.pdf

Collected:
YYYY-MM-DD

Title:
...

Author:
...

Creation Date:
...

Modification Date:
...

Relevant Finding:
...

New Pivot:
...

Confidence:
Medium
```

---

# 43. Fact vs Inference

This is one of the most important parts.

### Fact

The document lists:

```text
Author: Fawad Qureshi
```

### Inference

I believe this may connect the document to the target.

Those are not the same thing.

I keep them separate in my notes.

---

# 44. Don't Publish Everything You Find

Just because information is publicly accessible doesn't mean I need to dump it into a report.

I focus on information relevant to the investigation.

I avoid unnecessarily publishing:

* Private contact details
* Sensitive personal information
* Credentials
* Authentication information
* Personal addresses
* Information that could create unnecessary harm

Public availability and responsible disclosure are two different things.

---

# 45. Common Mistakes

### Mistake 1

Assuming a document author is automatically the target.

Wrong.

### Mistake 2

Assuming metadata is always accurate.

Wrong.

### Mistake 3

Treating a copied PDF as an independent source.

Wrong.

### Mistake 4

Ignoring publication dates.

Wrong.

### Mistake 5

Publishing every piece of personal information found.

Unnecessary.

### Mistake 6

Trusting search-engine snippets without opening the original source.

Bad practice.

---

# 46. My Point of View

A public document can look completely harmless.

But inside one file I might find:

```text
Name
↓
Organization
↓
Project
↓
Date
↓
Website
↓
Public email
↓
GitHub
↓
New domain
```

That's why I never look at a document as just a document.

I look at it as a **collection of potential pivots**.

But I also know when to stop.

If a document contains something sensitive that isn't relevant to the investigation, I don't need to collect or publish it just because I technically can see it.

Good OSINT is not about collecting the maximum amount of information.

It's about collecting the **right information, proving where it came from, and understanding what it actually means.**

---

# Final Rule

**Find the public document. Preserve it. Extract the useful clues. Follow the pivots. Verify every connection.**

Don't confuse metadata with proof.

Don't confuse a copied document with an independent source.

Don't publish sensitive information just because you found it.

**Search → Find → Extract → Pivot → Correlate → Verify → Document**
