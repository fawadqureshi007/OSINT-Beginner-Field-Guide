
# My OSINT Methodology

This is how I personally approach OSINT.

I don't believe OSINT is:

run 10 tools → copy results → make a report.

That is the easy part.

The difficult part is knowing what to search next, what to ignore, what to connect, and what you can actually prove.

My basic rule is:

**Collect → Pivot → Correlate → Verify → Document**

---

# 1. I Start With The Smallest Clue

If all I have is an Instagram username, I don't need the person's whole identity before starting.

I start with whatever is already public.

For example:

```text
Username
Display Name
Bio
Profile Picture
Public Links
Posts
Videos
Followers
Following
Comments
Mentions
Tags
Highlights
````

I write these down first.

I don't immediately assume that the name in the bio is the real identity, or that another account using the same username belongs to the same person.

Everything starts as a clue.

---

# 2. Username Is My First Pivot

I normally search the exact username first.

Example:

```text
"username"
```

Then I start combining it with whatever else I already know.

```text
"username" Instagram
"username" GitHub
"username" LinkedIn
"username" Facebook
"username" cybersecurity
"username" "Full Name"
```

I also check username variations.

People reuse usernames, slightly change them, add numbers, remove characters, or keep an old username on another platform.

This is where tools like Sherlock and Maigret become useful.

But I don't treat their output as truth.

They are basically giving me places to look.

---

# 3. Same Username Does Not Mean Same Person

This is one of the biggest mistakes beginners make.

If I find:

```text
Instagram → redteamerx
GitHub → redteamerx
Reddit → redteamerx
```

I don't immediately write:

> "I found three accounts belonging to the target."

No.

I start comparing them.

```text
Username
+
Name
+
Profile Picture
+
Bio
+
Website
+
Organization
+
Interests
+
Activity
+
Cross-links
```

If only the username matches, I keep it unconfirmed.

If several independent identifiers match, my confidence becomes stronger.

---

# 4. Don't Stop At The Target Profile

This is where I personally spend a lot of time.

If I'm investigating a public social-media account, I don't only look at the target.

I look at the public network around it.

Followers.

Following.

Comments.

Mentions.

Tags.

Collaborations.

Public interactions.

Repeated accounts.

The target may not publish a useful clue directly.

Someone connected to the target might.

For example:

```text
Target
↓
Following
↓
Public account
↓
Tagged photo
↓
Event
↓
Location
```

Or:

```text
Target
↓
Public interaction
↓
Another account
↓
Organization
↓
Website
↓
New identifier
```

That is a pivot.

---

# 5. Followers Are Not Just Numbers

A follower list can become a map.

I look for patterns.

Not just:

"Who follows this account?"

I ask:

"Who repeatedly appears around this account?"

I check publicly visible:

* Repeated commenters
* Frequently tagged accounts
* Collaborators
* Public friends
* Professional contacts
* Event accounts
* Organizations
* Project accounts
* Accounts appearing in multiple posts
* Accounts repeatedly mentioned

I don't call someone a friend, relative or colleague just because they follow the target.

That is an assumption.

I need public evidence before making that connection.

---

# 6. Following Can Give Better Pivots

Sometimes the following list is more useful than the target's own profile.

A person may follow:

```text
University
Company
Security community
Local organization
Event
Conference
Project
Friend
Professional contact
```

Those accounts can reveal new identifiers.

For example:

```text
Target
↓
Following
↓
Security conference
↓
Event page
↓
Public attendee information
↓
New identifier
```

I don't blindly collect everything.

I follow the paths that actually produce useful information.

---

# 7. Profile Picture Is Another Pivot

I save publicly available images and test them.

Depending on the image, I may use:

* Google Lens
* Bing Visual Search
* Yandex
* TinEye

I'm looking for:

```text
Same image
Older profile
Other public account
Website
Article
Public appearance
```

But reverse-image search is not magic.

A result can be visually similar without being the same person.

So I manually compare it.

---

# 8. Sometimes The Profile Picture Is Useless

This happened during my own investigation.

The profile picture did not give me a useful result.

Instead of forcing it, I moved to another public image.

That image produced better results.

This is important:

**Don't become attached to one pivot.**

If a pivot is dead:

```text
Stop
↓
Go back
↓
Choose another public clue
```

OSINT is not supposed to be a straight line.

---

# 9. Look At The Actual Content

I don't only read captions.

I look at the whole image or video.

The background can be more useful than the subject.

I check for:

```text
Buildings
Roads
Signs
Shop names
Landmarks
Architecture
Mountains
Events
Uniforms
Vehicles
Weather
Street layouts
Logos
Public locations
```

Someone may never write:

> "I'm in Islamabad."

But a picture can contain enough visual information to make Islamabad a reasonable location assessment.

---

# 10. GEOINT

This is where I move from:

"Who is this?"

to:

"Where could this content have been created?"

I tested public images and videos with Google Lens.

In my own case, multiple pieces of content produced Islamabad-related results.

I didn't take the first result and call it confirmed.

I tested more content.

The result was:

```text
Media 1 → Islamabad indication
Media 2 → Islamabad indication
Media 3 → Islamabad indication
```

That made the Islamabad association more interesting.

My report would say:

**Islamabad area indication based on multiple visual results.**

Not:

**Exact location confirmed.**

There is a huge difference.

---

# 11. Metadata Comes Before Guessing

If I have the original media, I check metadata.

I use ExifTool and look for:

```text
GPS
Creation Time
Modification Time
Camera
Device
Software
Image Information
Video Information
Encoding
```

Example:

```bash
exiftool -a -u -g1 file.mp4
```

If GPS exists, that's a very useful clue.

If GPS doesn't exist, I don't waste the entire investigation trying to recover something that isn't there.

I move to visual intelligence.

---

# 12. No Metadata Doesn't Mean No Intelligence

This is something I learned during the investigation.

A file can have no useful GPS information and still expose a location through the actual content.

For example:

```text
No GPS
↓
Look at image
↓
Identify building
↓
Identify road
↓
Compare environment
↓
GEOINT
```

So I don't treat:

**No EXIF**

as:

**No location intelligence.**

---

# 13. Search Engines Are Also OSINT Tools

Sometimes I don't need a special OSINT tool.

A search engine plus good queries can produce better information.

I combine identifiers.

Example:

```text
"Full Name" "username"
"Full Name" cybersecurity
"Full Name" "offensive security"
"username" GitHub
"username" LinkedIn
```

Then I add restrictions when needed:

```text
site:github.com
site:linkedin.com
site:facebook.com
```

The important thing is not making hundreds of searches.

It's making the next search based on what I already discovered.

---

# 14. Every Finding Should Create A New Question

This is probably the biggest thing in my workflow.

If I find a GitHub account, I ask:

> What else can this GitHub account give me?

If I find a domain:

> What public infrastructure is connected to it?

If I find an organization:

> What other public identifiers does the organization expose?

If I find an event:

> What public information is associated with that event?

If I find another account:

> Why do I believe this account belongs to the same person?

Every answer should give me another question.

---

# 15. Domain Pivot

If a public domain appears, I change direction.

My flow becomes:

```text
Domain
↓
RDAP / WHOIS
↓
DNS
↓
Subdomains
↓
Certificate Transparency
↓
Technology
↓
Public repositories
↓
Historical assets
```

I don't perform this just because I know the tools.

If there is no domain, I skip it.

Forcing a pivot usually creates noise.

---

# 16. Public Documents

If I have a reliable public name or organization, I can search for public documents.

For example:

```text
"Full Name" filetype:pdf
"Full Name" filetype:doc
"Full Name" filetype:ppt
```

I'm looking for legitimately public material such as:

* Research
* Presentations
* Reports
* Public project documents
* Conference material
* Academic material

A document can expose another identifier.

For example:

```text
Name
↓
PDF
↓
Organization
↓
Project
↓
Website
↓
New account
```

Again, another pivot.

---

# 17. GitHub Is A Pivot, Not Just A Profile

If I find a public GitHub account, I don't stop at the username.

I can examine the public footprint:

```text
Profile
↓
Repositories
↓
Projects
↓
Organizations
↓
Public documentation
↓
Website
↓
Public commit history
```

The important thing is to stay within information that is actually public.

I'm interested in correlation, not accessing private accounts or private data.

---

# 18. Historical OSINT

I also think about the target's older public footprint.

People change:

* Usernames
* Bios
* Profile pictures
* Websites
* Organizations
* Projects

So the current profile is not necessarily the complete story.

A historical public page can give me a username that the person no longer uses.

That username can become another pivot.

```text
Current profile
↓
Old username
↓
Old public account
↓
Older profile picture
↓
Historical information
```

---

# 19. The Social Graph Can Become Huge

I don't need to investigate every person connected to the target.

I follow useful branches.

For example:

```text
Target
 ├── Account A
 │    └── Organization
 │         └── Website
 │
 ├── Account B
 │    └── Public event
 │         └── Location
 │
 └── Account C
      └── Project
           └── GitHub
```

Then I compare the branches.

If several independent branches point toward the same identity, organization, project or location, confidence increases.

---

# 20. Correlation Is The Real Skill

A tool can tell me:

> "This username exists."

That's not enough.

Another tool can tell me:

> "This image looks similar."

Still not enough.

Google Lens can tell me:

> "This looks like Islamabad."

Still not enough for an exact claim.

But when multiple independent public clues support the same conclusion, the finding becomes much stronger.

That's correlation.

---

# 21. I Separate Facts From Assumptions

I keep three categories.

### FACT

Something directly supported by the public source.

Example:

```text
The account publicly uses @redteamerx.
```

### INFERENCE

Something I conclude from multiple clues.

Example:

```text
The media appears to be associated with the Islamabad area.
```

### UNCONFIRMED

Something that looks possible but doesn't have enough evidence.

Example:

```text
A different account uses the same username.
```

I don't mix these together.

---

# 22. Confidence

I normally think about confidence like this:

```text
LOW
↓
One weak clue

MEDIUM
↓
Multiple supporting clues

HIGH
↓
Independent sources directly support the same fact
```

Confidence should come from evidence.

Not from how convincing the story sounds.

---

# 23. False Positives

OSINT has a huge false-positive problem.

The biggest examples are:

```text
Same username
Same name
Similar profile picture
Similar interests
Similar location
```

Any one of these can be completely unrelated.

That's why I always ask:

> "What else proves this connection?"

If I cannot answer that, I keep it unconfirmed.

---

# 24. My Investigation Notes

For useful findings I record:

```text
Finding:
Source:
URL:
Date:
Evidence:
New identifier:
Next pivot:
Confidence:
Fact / Inference / Unconfirmed:
```

This prevents the investigation from becoming a mess after dozens of pivots.

---

# 25. My Full Workflow

The complete flow I use is basically:

```text
START
  ↓
Collect public information
  ↓
Username enumeration
  ↓
Search engines
  ↓
Identity correlation
  ↓
Other public accounts
  ↓
Followers / Following
  ↓
Social graph
  ↓
Images
  ↓
Reverse-image search
  ↓
Public posts / videos
  ↓
GEOINT
  ↓
Metadata
  ↓
Public documents
  ↓
Technical footprint
  ↓
Historical footprint
  ↓
Correlation
  ↓
Verification
  ↓
Document findings
```

But in a real investigation I don't follow this like a checklist.

I jump between pivots depending on what I find.

---

# 26. The Part Beginners Usually Miss

Beginners usually ask:

> "Which OSINT tool should I use?"

My answer is:

**First ask what information you already have.**

If you have a username, search the username.

If you have an image, investigate the image.

If you have a domain, investigate the domain.

If you have a public connection, investigate the connection.

Don't run every tool just because it exists.

The clue decides the tool.

---

# 27. My Rule For Tools

I use tools to make the investigation faster.

I don't use tools to replace thinking.

For me:

```text
Tool → Lead
Manual research → Context
Correlation → Meaning
Verification → Confidence
```

That's the difference.

---

# 28. Final Rule

The most important rule I follow is:

**Never let the tool decide the conclusion for you.**

A tool can be wrong.

A username can be reused.

An image can be copied.

A search result can be unrelated.

A location model can make a wrong prediction.

A metadata field can be missing.

So I collect the result, check it manually, compare it with another source, and only then decide how useful it actually is.

The goal isn't to collect someone's entire life.

The goal is to understand what is publicly exposed, how those pieces connect, and which conclusions can actually be supported by evidence.

For me, that's OSINT.

**Find the clue.
Follow the pivot.
Connect the dots.
Kill the false positives.
Verify everything.**

