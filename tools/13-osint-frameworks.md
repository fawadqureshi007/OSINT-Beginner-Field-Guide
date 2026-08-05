# 13 — OSINT Frameworks

## My Approach

I don't use OSINT tools randomly.

There are thousands of tools, websites and databases available, but running 20 tools on every target usually creates more noise than intelligence.

My approach is simple:

**Start with what I know → choose the right category → run the relevant tools → collect useful results → create new pivots → verify everything.**

The tool is not the investigation.

**The investigation is the thinking between the tools.**

---

# 1. What Is an OSINT Framework?

An OSINT framework is basically a structured collection of resources that helps you find the right tool or source for a particular type of investigation.

Instead of searching randomly for:

```text
OSINT tool for username
OSINT tool for email
OSINT tool for domains
```

I can use an OSINT framework to find resources organized by category.

Typical categories include:

```text
Username
Email
Social Media
Search Engines
Domains
DNS
IP Addresses
Geolocation
Documents
Images
People
Companies
Archives
Breaches
Technical Infrastructure
```

---

# 2. One Framework Does Not Give You the Answer

This is something beginners often misunderstand.

If a framework lists 50 tools under:

```text
Username
```

that doesn't mean I should run all 50.

I first ask:

**What information do I already have?**

For example:

```text
Username:
redteamerx
```

Now username enumeration makes sense.

If I only have:

```text
example.com
```

I don't start with username tools.

I move toward:

```text
Domain
↓
DNS
↓
Subdomains
↓
Certificates
↓
Technology
↓
Public infrastructure
```

The starting clue determines the path.

---

# 3. My Pivot-Based Method

I use this basic model:

```text
Starting Identifier
        ↓
Relevant OSINT Category
        ↓
Tool / Search
        ↓
New Identifier
        ↓
New Category
        ↓
Verification
        ↓
New Pivot
```

Example:

```text
Instagram Username
↓
Username Search
↓
GitHub Account
↓
Repository
↓
Domain
↓
DNS
↓
Certificate
↓
Historical Domain
```

This is much better than blindly running every OSINT tool.

---

# 4. Start With the Strongest Identifier

Not every clue has the same value.

For example:

```text
Common Name
```

can produce thousands of results.

A unique username may be much more useful.

A unique domain can be even stronger.

A public email address can provide another strong pivot.

I normally prioritize:

```text
Unique Username
↓
Unique Email
↓
Domain
↓
Exact Name + Context
↓
Organization
↓
Project
↓
General Search Terms
```

The exact order depends on the investigation.

---

# 5. Username Investigation

If I have:

```text
redteamerx
```

I can use the username tools from the earlier chapters.

For example:

```text
Sherlock
Maigret
Search Engines
Manual Platform Search
```

But I don't stop after getting results.

I compare:

```text
Username
Name
Profile Image
Bio
Website
Organization
Projects
Public Activity
```

This is how I reduce false positives.

---

# 6. Search Engines Are Still Important

Even when I have automated tools, I still manually search.

Example:

```text
"redteamerx"
```

Then:

```text
"redteamerx" cybersecurity
```

Then:

```text
"redteamerx" GitHub
```

Then:

```text
"redteamerx" LinkedIn
```

The reason is simple:

**A tool only checks what it knows how to check.**

Search engines may discover something the tool doesn't.

---

# 7. Don't Trust Automated Results Blindly

Suppose a tool returns:

```text
redteamerx
GitHub
Reddit
Instagram
Forum
```

I don't write:

**Target has five accounts.**

I write:

**Five potential username matches were discovered.**

Then I verify each one.

---

# 8. False Positives

This is one of the biggest problems in OSINT.

Two completely different people can use:

```text
redteamerx
```

Therefore:

```text
5 username results
≠
5 confirmed accounts
```

I look for multiple matching indicators.

For example:

```text
Same username
+
Same profile image
+
Same public name
+
Same website
+
Same organization
```

The more independent connections I have, the stronger the attribution becomes.

---

# 9. My Confidence System

I normally classify findings as:

### Low

Only one weak indicator.

```text
Same username
```

### Medium

Several matching public indicators.

```text
Same username
+
same name
+
similar bio
```

### High

Multiple independent sources support the same connection.

```text
Same username
+
same name
+
same website
+
same organization
+
independent public confirmation
```

This prevents me from turning guesses into facts.

---

# 10. When to Change Categories

Suppose I start with:

```text
Username
```

and discover:

```text
example.com
```

I stop focusing only on usernames.

Now the domain becomes my next pivot.

```text
Username
↓
Website
↓
Domain OSINT
```

Then I may move to:

```text
DNS
Subdomains
Certificates
Technology
Repositories
Archives
```

This is what I mean by **pivoting**.

---

# 11. Domain Pivot

If I discover:

```text
example.com
```

I move toward:

```text
DNS
WHOIS/RDAP
Subdomains
Certificate Transparency
Historical DNS
Web Technologies
Archives
Public Repositories
```

Each result can create another pivot.

---

# 12. Email Pivot

If a public source gives me:

```text
example@example.com
```

I don't immediately search for sensitive information.

I use it as a public identifier.

I can check where that address is publicly referenced:

```text
"example@example.com"
```

Then:

```text
"example@example.com" GitHub
```

or:

```text
"example@example.com" site:example.com
```

The goal is to correlate public information.

---

# 13. GitHub Pivot

If I find a public GitHub account:

```text
GitHub
↓
Username
↓
Repositories
↓
Commits
↓
Projects
↓
Public email
↓
Domains
```

I can then move into GitHub OSINT.

I don't automatically assume every repository associated with a similar username belongs to the same person.

---

# 14. Social Media Pivot

A public social profile can provide:

```text
Username
Name
Bio
Website
Organization
Public posts
Public interactions
Public links
```

I use those as pivots.

For example:

```text
Instagram
↓
Website
↓
GitHub
↓
Project
```

or:

```text
Instagram
↓
Username
↓
Other public platform
```

---

# 15. Image Pivot

If I have a public profile image or other publicly available image:

```text
Image
↓
Reverse Image Search
↓
Matching public pages
↓
Original/older source
↓
New identifiers
```

This is where the reverse-image chapter becomes useful.

I don't treat visually similar images as automatic proof.

---

# 16. Document Pivot

If I find a public PDF:

```text
PDF
↓
Author
↓
Project
↓
Organization
↓
Website
```

Then:

```text
Metadata
↓
Additional clues
```

Again, every connection gets verified.

---

# 17. GEOINT Pivot

If public media contains useful visual clues:

```text
Image
↓
Landmark
↓
Road
↓
Building
↓
Public location
```

I can investigate the location separately.

I don't assume:

```text
Photo location = person's home
```

A photo can simply show where an event happened.

---

# 18. Archive Pivot

If a current page doesn't contain useful information, historical sources can sometimes provide context:

```text
Current Website
↓
Archived Version
↓
Old Username
↓
Old Bio
↓
Old Project
```

That old identifier can become a new search pivot.

---

# 19. Organization Pivot

If I discover:

```text
Company / University / Organization
```

I investigate its public footprint:

```text
Organization
↓
Website
↓
Employees / public profiles
↓
Projects
↓
Documents
↓
Domains
↓
Public repositories
```

This can connect information that wasn't directly visible on the original target profile.

---

# 20. Tool Selection

My rule is:

**Use the smallest number of tools that can answer the question properly.**

For example:

### Username

```text
Sherlock
Maigret
Search Engines
Manual verification
```

### Domain

```text
DNS tools
RDAP
Certificate Transparency
Technology identification
Archives
```

### Documents

```text
ExifTool
pdfinfo
pdftotext
OCR
```

### Images

```text
Google Lens
Bing Visual Search
Yandex
TinEye
ExifTool
```

The exact tool depends on the clue.

---

# 21. Manual + Automated OSINT

I prefer combining both.

### Automated

Good for:

* Speed
* Enumeration
* Large numbers of sources
* Repetitive checks

### Manual

Good for:

* Context
* Verification
* Correlation
* Understanding relationships
* Removing false positives

My workflow is usually:

```text
Automated Discovery
↓
Manual Verification
↓
Independent Source
↓
Correlation
```

---

# 22. Don't Run Everything

A beginner may think:

```text
Run Sherlock
Run Maigret
Run every scanner
Run every OSINT tool
Run every API
```

That can create hundreds or thousands of results.

More results don't necessarily mean better intelligence.

I would rather have:

```text
10 strong findings
```

than:

```text
1,000 unverified results
```

---

# 23. Record Every Pivot

I maintain notes like:

```text
Starting username:
redteamerx

Found:
GitHub profile

New pivot:
GitHub username

Found:
Project name

New pivot:
Project

Found:
Website

New pivot:
example.com
```

This creates an investigation chain.

---

# 24. Build an Intelligence Graph

A simple graph might look like:

```text
                Username
                   |
          +--------+--------+
          |                 |
       Instagram         GitHub
          |                 |
       Website           Project
          |                 |
        Domain          Repository
          |
       Subdomain
          |
      Certificate
```

The graph helps me understand how individual clues connect.

---

# 25. Evidence Table

For serious investigations I maintain:

| Finding        | Source         | Pivot    | Confidence |
| -------------- | -------------- | -------- | ---------- |
| Username match | Public profile | Username | Medium     |
| Website        | Public profile | Domain   | High       |
| Project        | GitHub         | Project  | High       |
| Location clue  | Public media   | GEOINT   | Medium     |

This keeps the investigation organized.

---

# 26. Fact vs Inference

This is one of my biggest rules.

### Fact

```text
The public profile links to example.com.
```

### Inference

```text
The person probably owns example.com.
```

The first is directly observable.

The second needs additional evidence.

I never write an inference as if it were a confirmed fact.

---

# 27. My Verification Rule

For important findings:

```text
Discovery
↓
Second Source
↓
Context Check
↓
Timeline Check
↓
Final Confidence
```

If I cannot verify something, I mark it:

```text
Unconfirmed
```

instead of forcing the conclusion.

---

# 28. Tool Results Are Leads

This is especially important with:

* Username tools
* People-search tools
* Automated scanners
* Reverse-image tools
* AI tools

They can help me find leads.

They don't replace human verification.

My rule:

> **Tool output creates a lead. Evidence creates confidence.**

---

# 29. OSINT Frameworks I Use

Frameworks can help discover resources for:

```text
Username
Email
People
Social Media
Domains
DNS
IP
Images
Documents
Geolocation
Companies
Archives
```

I use them as a **directory**, not as an automatic investigation engine.

---

# 30. My Decision Tree

When I receive a new target:

```text
What do I know?
        ↓
Username?
        ↓
Username OSINT
        ↓
New account?
        ↓
Social OSINT
        ↓
Website?
        ↓
Domain OSINT
        ↓
Email?
        ↓
Email OSINT
        ↓
Image?
        ↓
Image OSINT
        ↓
Document?
        ↓
Document + Metadata OSINT
        ↓
Historical information?
        ↓
Archive OSINT
        ↓
Location clue?
        ↓
GEOINT
```

Not every investigation follows every branch.

I only take the branch that makes sense.

---

# 31. My Biggest OSINT Lesson

The best tool isn't always the most advanced tool.

Sometimes the most useful discovery comes from something simple:

```text
Google Search
```

or:

```text
A public profile bio
```

or:

```text
A GitHub README
```

or:

```text
A PDF
```

or:

```text
An old public page
```

The important part is recognizing the pivot.

---

# 32. Don't Chase Every Result

If I find something unrelated to the investigation, I don't keep following it just because it looks interesting.

I ask:

**Does this result create a useful connection to my target?**

If no:

```text
Ignore it.
```

If yes:

```text
Record it.
Verify it.
Pivot from it.
```

This keeps the investigation clean.

---

# 33. My Recommended Beginner Workflow

If someone is new to OSINT, I would start with:

```text
1. Username
2. Search Engines
3. Social Media
4. Reverse Image
5. Domain
6. DNS
7. Public Documents
8. Metadata
9. Archives
10. GEOINT
```

Learn how these connect before trying dozens of advanced tools.

---

# 34. Advanced Workflow

Once the basics are comfortable:

```text
Identifier
↓
Automated Enumeration
↓
Manual Verification
↓
Social Correlation
↓
Domain Discovery
↓
Infrastructure Enumeration
↓
Historical Research
↓
Document Research
↓
Visual Analysis
↓
Relationship Mapping
↓
Timeline
↓
Evidence Validation
↓
Final Intelligence Report
```

---

# 35. My Point of View

OSINT is not:

**"Which tool can find the most information?"**

For me, OSINT is:

**"Which clue can give me the next useful pivot?"**

A username can lead to a GitHub account.

A GitHub account can lead to a project.

A project can lead to a domain.

A domain can lead to certificates.

A certificate can reveal another public hostname.

A hostname can lead to an archived website.

An archived website can reveal an old username.

And that username can take the investigation somewhere completely different.

That's the real power of OSINT.

**You don't collect random data. You build connections.**

---

# Final Rule

```text
Don't:
Run Everything → Collect Everything → Assume Everything

Do:
Start With a Clue
↓
Choose the Right Tool
↓
Find a Lead
↓
Verify It
↓
Create a Pivot
↓
Follow the Pivot
↓
Document the Evidence
```

**Tools give you results.**

**Correlation gives you intelligence.**

**Verification gives you confidence.**
