# OSINT Beginner Field Guide

A practical beginner-friendly guide to performing Open Source Intelligence (OSINT) from publicly available information.

This guide is based on my own practical self-OSINT investigation. The main idea is simple:

> OSINT is not just about running tools. The real work is connecting small pieces of public information and verifying whether they actually belong together.

---

## 1. Starting Point

Imagine you meet someone on Instagram and only know their public username and profile.

Your starting information may include:

- Username
- Display name
- Bio
- Profile picture
- Public links
- Public posts
- Public highlights
- Public followers and following

The goal is not to collect everything about the person.

The goal is to determine what useful information is already publicly exposed and how different pieces of information connect.

### Basic flow

**Instagram → Username → Other Accounts → Identity Clues → Relationships → Location → Professional Footprint → Technical Footprint → Historical Footprint → Verification**

---

## 2. Start With The Original Profile

Before using any tool, manually inspect the target profile.

Record publicly visible information such as:

- Username
- Display name
- Bio
- Profile picture
- Links
- Public posts
- Highlights
- Mentions
- Tags
- Public followers/following
- Other usernames mentioned in the profile

Don't immediately decide what each piece means.

First collect the information.

---

## 3. Username OSINT

The username is usually one of my first pivots.

Start with an exact search:

`"username"`

Then expand it:

`"username" Instagram`  
`"username" GitHub`  
`"username" LinkedIn`  
`"username" Facebook`  
`"username" Reddit`

Also search username variations.

The objective is not simply to find the same username somewhere else.

The objective is to find a **new identifier** that can be verified and used as the next pivot.

For example:

**Username → Other Public Account → Name → Organization → Website**

---

## 4. Username Enumeration

Tools such as Sherlock and Maigret can help enumerate where a username may exist across public platforms.

They are useful for generating leads.

However:

> A username match is not identity confirmation.

For example, if a tool returns 40 results, that does not mean all 40 accounts belong to the target.

A username can be reused by completely different people.

I compare additional indicators such as:

- Same username
- Same name
- Same profile picture
- Same bio
- Same website
- Same organization
- Similar public interests
- Consistent timeline

If there is only a username match, I mark it as **unconfirmed**.

---

## 5. Search Engines

Search engines are one of the most useful OSINT tools because they can connect information from different websites.

Start with:

`"username"`

Then search discovered identifiers:

`"Full Name"`  
`"Full Name" "username"`  
`"Full Name" cybersecurity`  
`"Full Name" "offensive security"`

You can also search specific platforms:

`"username" site:github.com`

`"username" site:linkedin.com`

`"username" site:facebook.com`

I record useful discoveries instead of collecting every search result.

---

## 6. Followers & Following

This is one of the areas I pay particular attention to when the target's account is public.

Don't just inspect the target's profile.

Look at publicly visible followers and following and search for relationships and repeated patterns.

Things I look for include:

- Frequently interacting accounts
- Repeated commenters
- Public mentions
- Tagged photos
- People appearing repeatedly around the target
- Public colleagues
- Public classmates
- Public communities
- Organizations
- Event accounts
- Project-related accounts

The goal is not to investigate every person.

The goal is to find a **useful pivot**.

For example:

**Target → Frequently interacting account → Public profile → Organization → Website → New identifier**

A single interaction is not enough to establish a relationship. I look for repeated and independently supported evidence.

---

## 7. Look Around The Target

Sometimes the target's own account reveals very little.

The useful clue may exist around them.

A publicly connected account can reveal:

- Name
- Organization
- School
- University
- Workplace
- Project
- Website
- Event
- Another username

That information can become the next pivot.

> Don't only investigate the target. Investigate the public information surrounding the target.

---

## 8. Posts, Highlights, Tags & Mentions

Public content can contain clues that the uploader may not have considered important.

I look at:

- Posts
- Highlights
- Tagged photos
- Mentions
- Comments
- Older content
- Public events

I pay attention to background information such as:

- Road signs
- Buildings
- Landmarks
- Company logos
- School signs
- Event banners
- Vehicles
- Architecture
- Streets
- Store names
- Public infrastructure

Sometimes one small visual detail becomes a completely new pivot.

---

## 9. Reverse Image Search

If a publicly available profile picture or image is useful, I can test it using reverse-image search services such as:

- Google Lens
- Bing Visual Search
- Yandex Images
- TinEye

I look for:

- Same image
- Cropped versions
- Older versions
- Other public profiles
- Websites
- Articles
- Public appearances

A reverse-image result is still a lead.

I manually compare the result before connecting it to the target.

---

## 10. GEOINT & Location Analysis

Location is another important pivot.

I check publicly available clues such as:

- Country
- City
- Workplace
- University
- Events
- Public geotags
- Landmarks
- Buildings
- Road signs
- Background details

I don't treat a single location result as absolute proof.

For example:

**Public bio + workplace + university + visual landmark + independent location result**

When multiple independent clues point toward the same area, confidence becomes stronger.

However:

> A visual geolocation result is a lead, not automatically an exact current location.

---

## 11. Metadata Analysis

If I obtain an original public media file, I check whether useful metadata is still available.

Possible information includes:

- GPS coordinates
- Capture date/time
- Device information
- Software
- Media creation information

Tools such as ExifTool can help inspect this information.

But metadata is often removed or modified when media is uploaded to social-media platforms or shared through messaging applications.

Therefore:

**No GPS metadata ≠ No location clue**

It simply means that particular file did not provide an embedded GPS record.

I then move toward visual analysis and other independent public sources.

---

## 12. Public Documents

If I discover a reliable name, organization, project or other identifier, I can search for publicly indexed documents.

Examples:

`"Full Name" filetype:pdf`

`"Full Name" filetype:doc`

`"Full Name" filetype:ppt`

I don't force this step.

If there is no reliable identifier, I move to another pivot.

---

## 13. Professional Footprint

If a professional identity is discovered, I look at publicly available information such as:

- Job title
- Organization
- Education
- Projects
- Portfolio
- Articles
- Conferences
- Professional profiles
- Public websites

A professional profile can create another pivot:

**Name → Organization → Website → Domain → Technical Footprint**

---

## 14. Domain & DNS Pivot

If a legitimate public domain is discovered, I can move into the technical footprint.

The general flow is:

**Domain → Subdomains → DNS → Certificates → Technologies → Public Repositories → Historical Assets**

I don't start technical reconnaissance without first establishing a useful public pivot.

---

## 15. WHOIS / RDAP

For a discovered domain, public registration information may provide useful context.

Depending on privacy settings and the registry, information may include:

- Registrar
- Registration dates
- Nameservers
- Domain status
- Public organization information

Privacy protection can hide registrant information, so I don't expect every domain to reveal an owner.

---

## 16. Certificate Transparency

Certificate Transparency logs can sometimes reveal hostnames associated with a domain.

A basic pivot can look like:

**Domain → Certificate → Hostname → Subdomain**

This can expose additional publicly visible infrastructure that wasn't obvious from the main website.

---

## 17. GitHub / GitLab

If a developer identity or username is discovered, public repositories can become another pivot.

I look at publicly available:

- Repositories
- Projects
- Profile information
- Public commits
- Documentation
- Organizations
- Publicly disclosed domains

Again, a matching username alone is not enough.

---

## 18. Historical Footprint

People change usernames, websites and profiles.

Historical public sources can sometimes reveal:

- Previous usernames
- Older profiles
- Archived pages
- Historical websites
- Old bios
- Former public affiliations

Historical information must always be considered according to its date.

An old profile does not automatically represent the person's current situation.

---

## 19. Public Data Exposure

Depending on the scope of the investigation, I may check information that has already been publicly disclosed.

Examples include:

- Public email addresses
- Public contact information
- Public documents
- Publicly disclosed records
- Public breach/disclosure information

I verify the source and avoid collecting unnecessary sensitive information.

---

# 20. Correlation

This is where OSINT becomes much more interesting.

Instead of looking at isolated results, I connect useful discoveries.

Example:

**Username → Other Account → Name → Professional Profile → Organization → Website → Domain → Technical Footprint**

Another example:

**Target → Public Interaction → Connected Account → Event → Location → Date → Independent Confirmation**

The objective isn't to build the biggest graph.

The objective is to build a graph where important connections are supported by evidence.

---

# 21. Evidence

For every useful discovery, I document:

| Field | What I record |
|---|---|
| Source | Where the information came from |
| URL | Original public source |
| Finding | What I discovered |
| Date | When it was observed |
| New Identifier | New pivot discovered |
| Confidence | High / Medium / Low |
| Classification | Fact / Inference |
| Verification | How I confirmed it |

This makes the investigation easier to reproduce and prevents me from losing track of where information came from.

---

# 22. Fact vs Inference

This distinction is extremely important.

### Fact

Something directly supported by a public source.

Example:

> A public profile lists Islamabad.

### Inference

A conclusion based on multiple observations.

Example:

> Several independent visual clues appear consistent with the Islamabad area.

I keep facts and inferences separate.

---

# 23. Confidence

### High

Multiple independent public sources support the same finding.

### Medium

Several indicators support the finding, but independent confirmation is limited.

### Low

It is only a possible lead and could belong to someone else.

A tool returning a result does not automatically make that result high confidence.

---

# 24. False Positives

One of the biggest problems in OSINT is incorrect attribution.

Never assume:

**Same username = Same person**

**Same name = Same person**

**Same profile picture = Same person**

**Same city = Same person**

**Same organization = Same person**

**One location result = Exact location**

These are indicators.

They require correlation and verification.

---

# 25. Tools

Tools can make enumeration faster, but I don't let tools make the final decision.

Useful categories include:

- Username enumeration
- Search engines
- Social-media search
- Reverse-image search
- Metadata analysis
- Domain / DNS reconnaissance
- WHOIS / RDAP
- Certificate Transparency
- Public document search
- GitHub / GitLab search
- Web archives
- GEOINT
- Public disclosure databases

Tools change.

The methodology is more important than memorizing a tool list.

---

# 26. My Practical Rule

**Collect → Correlate → Verify → Document**

I don't run ten tools and blindly combine their outputs.

I use tools to generate leads.

Then I manually check whether those leads actually connect.

---

# 27. My Point Of View

One thing I realized during my own investigation is that OSINT is not just about running tools and waiting for results.

The real work starts when I manually connect the small pieces.

I start with the target's name, username, profile picture, bio and obvious identifiers.

Then I move through publicly visible followers, following, mentions, tags, comments and connected accounts.

Sometimes the target doesn't reveal anything directly.

A public connected account may reveal the missing identifier.

A public photograph may reveal a location.

A website may reveal an organization.

A username may reveal an old account.

An old account may reveal another identifier.

That's how the investigation keeps moving.

---

# 28. The Biggest Lesson

The most useful information isn't always hidden inside an OSINT tool.

Sometimes it is sitting in plain sight:

- A username
- A public connection
- An old post
- A profile picture
- A background sign
- A public document
- A website
- A repeated interaction

One clue may look useless by itself.

But when it connects with other independent public clues, the bigger picture starts becoming visible.

> **OSINT is not about collecting everything.**
>
> **It's about finding the right clues, connecting them, eliminating false positives, and verifying what actually holds up.**

---

# Final Rule

## Think like an investigator, not like a tool user.

Tools can find leads.

**You decide whether the leads actually connect.**

---

## Disclaimer

This repository is intended for educational OSINT research using publicly available information.

Only investigate accounts, systems and information where you have appropriate authorization or where the activity is lawful and ethical.

Respect privacy, platform rules and applicable laws.

