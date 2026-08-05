# 15 — Email OSINT

## My Approach

Email OSINT is not about finding an email and stopping there.

For me, an email is another **pivot**.

I want to know:

* Where does the email appear?
* What account is connected to it?
* What username is connected to it?
* Is it connected to a project?
* Is there a company?
* Is there a GitHub account?
* Does another public source confirm the connection?
* What new identifiers can I extract?

My general workflow is:

```text
Public Account
↓
Bio
↓
Public Links
↓
Platform
↓
Public Data
↓
New Identifier
↓
Email
↓
Independent Verification
↓
Document Findings
```

---

# 1. What Is Email OSINT?

Email OSINT means investigating information that is publicly available and connected to an email address.

Useful public sources include:

```text
Search engines
GitHub
GitLab
Personal websites
Public documents
Public profiles
Company pages
Project pages
Blogs
Forums
Public breach notifications
Historical public pages
```

The important part is **correlation**.

Finding an email somewhere is only a lead.

---

# 2. Start With a Public Identifier

I don't always start with an email.

Sometimes I start with:

```text
Username
Social-media account
Website
GitHub profile
Company
Project
```

Then I follow the public trail until an email becomes visible.

That is exactly how I approach real OSINT investigations.

---

# 3. Real Example — My Own Public OSINT Trail

For this example, I'm documenting my own public footprint.

I started from:

```text
h4cker_fawad
```

I didn't immediately search for an email.

First, I opened the public account and manually checked the profile.

I looked at:

```text
Username
Bio
Profile information
Public links
Projects
Public contact information
```

The bio contained **5 public links**.

That became my first major pivot.

---

# 4. Bio → 5 Public Links

The investigation started like this:

```text
h4cker_fawad
      ↓
Public Profile
      ↓
Bio
      ↓
5 Public Links
```

I opened the links individually.

This is important because I don't assume every link will provide the same information.

One may lead to:

```text
GitHub
```

another may lead to:

```text
Social Media
```

another may lead to:

```text
Website
```

The objective is to map the public footprint.

---

# 5. Why Manual Checking Matters

Automated tools are useful, but I don't start every investigation by running ten tools.

Sometimes the target has already connected everything publicly.

A simple profile can contain:

```text
Username
↓
Bio
↓
GitHub
↓
Website
↓
Other social accounts
```

If the information is already publicly connected, manual investigation can be faster and give better context.

---

# 6. GitHub Became My Important Pivot

One of the links from the bio led to GitHub.

I then moved from:

```text
h4cker_fawad
```

to:

```text
GitHub
```

I didn't just open the profile and leave.

I checked the public information available there.

I looked at:

```text
Username
Profile
Repositories
README files
Projects
Public links
Commit history
Public author information
```

This gave me another layer of information.

---

# 7. GitHub → Email

While analyzing the public GitHub information, I found another public identifier:

```text
cipherphantomofficial@gmail.com
```

This gave me the following chain:

```text
h4cker_fawad
      ↓
Public Bio
      ↓
5 Public Links
      ↓
GitHub
      ↓
Public GitHub Analysis
      ↓
Additional Public Information
      ↓
cipherphantomofficial@gmail.com
```

This is the important part of the case study.

I didn't randomly guess the email.

I reached it by following the public trail.

---

# 8. What I Check on GitHub

When I reach GitHub during an OSINT investigation, I normally inspect:

```text
Profile username
Display name
Bio
Repositories
Repository descriptions
README files
Website links
Social links
Public commits
Contributors
Public project information
```

I don't assume every piece of information belongs to the same person.

I correlate it.

---

# 9. Public Git History

If a repository is public, Git history can contain author information.

For a repository I am authorized to analyze:

```bash
git clone https://github.com/OWNER/REPOSITORY.git
```

Then:

```bash
cd REPOSITORY
```

View commit authors:

```bash
git shortlog -sne
```

Another useful command:

```bash
git log --format='%an <%ae>' | sort -u
```

This can show email addresses present in public Git history.

I treat these as public technical identifiers, not automatic proof of account ownership.

---

# 10. Search the Email

After discovering:

```text
cipherphantomofficial@gmail.com
```

I can perform an exact public search:

```text
"cipherphantomofficial@gmail.com"
```

Then search combinations such as:

```text
"cipherphantomofficial@gmail.com" GitHub
```

```text
"cipherphantomofficial@gmail.com" cybersecurity
```

```text
"cipherphantomofficial@gmail.com" project
```

```text
"cipherphantomofficial@gmail.com" website
```

The purpose is to discover additional public references.

---

# 11. Email → Username

The local part of an email can sometimes provide another search pivot.

For:

```text
cipherphantomofficial@gmail.com
```

the local part is:

```text
cipherphantomofficial
```

I can search:

```text
"cipherphantomofficial"
```

Then investigate possible public profiles using that identifier.

But:

```text
Same username
≠
Confirmed same person
```

It needs correlation.

---

# 12. Email → Search Engine

Exact searches are usually my first step.

Examples:

```text
"cipherphantomofficial@gmail.com"
```

```text
"cipherphantomofficial@gmail.com" site:github.com
```

```text
"cipherphantomofficial@gmail.com" filetype:pdf
```

```text
"cipherphantomofficial@gmail.com" project
```

Search engines can expose pages where an email was already publicly indexed.

---

# 13. Email → Public Documents

I also check whether the email appears in public documents.

Examples:

```text
"cipherphantomofficial@gmail.com" filetype:pdf
```

```text
"cipherphantomofficial@gmail.com" filetype:doc
```

If I find it, I check the surrounding information:

```text
Name
Organization
Project
Author
Website
Date
```

The surrounding context is often more valuable than the email itself.

---

# 14. Email → Website

If the email is associated with a public website, I inspect the page where it appears.

It could be:

```text
Contact page
Author page
Team page
Project page
Documentation
Blog
Company page
```

I record the source and context.

I don't just copy the email into my notes without knowing where it came from.

---

# 15. Email → Domain

If the address uses an organization domain:

```text
person@example.com
```

I extract:

```text
example.com
```

Then the investigation can continue:

```text
Email
↓
Domain
↓
Website
↓
DNS
↓
Subdomains
↓
Certificate Transparency
↓
Historical infrastructure
```

For Gmail addresses, this particular domain pivot isn't useful because `gmail.com` is a shared email provider.

---

# 16. Email → Company

Sometimes an email is publicly connected to a company.

For example:

```text
Public Profile
↓
Company Mention
↓
Company Website
↓
Company Email
```

This is the same concept I used when following the public links from my own account.

The company becomes a separate investigation target.

---

# 17. Public Email Enumeration Tools

Some tools can help automate parts of email OSINT.

Tools I would include in my toolkit are:

```text
Holehe
h8mail
theHarvester
Hunter
Have I Been Pwned
```

I don't treat automated results as final evidence.

Tool output is a **lead**.

---

# 18. Holehe

Holehe can check whether an email may be associated with accounts on supported services.

First check the installed version:

```bash
holehe --help
```

Then use the current syntax provided by that version.

Services can change their behavior, so an automated result should be manually verified.

---

# 19. h8mail

h8mail is designed for email-related OSINT collection.

Start with:

```bash
h8mail --help
```

Then use the syntax supported by your installed version.

The important question isn't:

**"What did the tool print?"**

It's:

**"Can I verify what the tool printed?"**

---

# 20. theHarvester

For public domain research:

```bash
theHarvester -d example.com -b all
```

Depending on the installed version and available sources, it may discover publicly indexed:

```text
Emails
Hosts
Subdomains
URLs
```

I verify important results independently.

---

# 21. Hunter

Hunter can help investigate publicly available professional email information associated with domains.

It can be useful for:

```text
Public email patterns
Domain-associated addresses
Professional contact information
```

An inferred email pattern is not proof that a specific person uses an address.

---

# 22. Have I Been Pwned

Have I Been Pwned can show whether an email appears in known breach records.

The distinction is important:

```text
Breach exposure
≠
Account access
```

I use breach information only as legitimate OSINT context.

I don't attempt to use leaked passwords or access accounts.

---

# 23. Gravatar

Some emails may have public Gravatar information associated with them.

The pivot can be:

```text
Email
↓
Public avatar
↓
Possible profile information
↓
Independent verification
```

A matching image alone isn't enough.

---

# 24. Search the Local Part

For:

```text
cipherphantomofficial@gmail.com
```

I can search:

```text
"cipherphantomofficial"
```

Then:

```text
"cipherphantomofficial" GitHub
```

```text
"cipherphantomofficial" Instagram
```

```text
"cipherphantomofficial" website
```

This can reveal public username reuse.

Again, reuse is a lead, not proof.

---

# 25. Search Email + Context

A plain email search may produce too many results.

I add context:

```text
"cipherphantomofficial@gmail.com" cybersecurity
```

```text
"cipherphantomofficial@gmail.com" Pakistan
```

```text
"cipherphantomofficial@gmail.com" GitHub
```

```text
"cipherphantomofficial@gmail.com" project
```

Context helps reduce unrelated results.

---

# 26. Historical Public References

An email may disappear from a current page but remain in older public material.

I can search for the exact email and investigate:

```text
Old websites
Old documentation
Old projects
Archived pages
Old repositories
Public publications
```

Historical information can reveal older identifiers.

---

# 27. Email → Historical Username

A useful chain can become:

```text
Email
↓
Old public page
↓
Old username
↓
Username investigation
↓
Current public profile
```

This is why I don't limit OSINT to current pages.

---

# 28. Don't Trust Search Snippets

If a search engine shows:

```text
"cipherphantomofficial@gmail.com"
```

I open the actual source.

I verify:

```text
Is the email actually present?
Who published it?
What is the context?
Is the page legitimate?
When was it published?
```

Search snippets can be outdated.

---

# 29. Evidence Collection

For every useful finding, I record:

```text
Identifier:
cipherphantomofficial@gmail.com

Source:
Public GitHub information

How I found it:
h4cker_fawad → bio → public links → GitHub → analysis

Context:
Publicly available information

Next pivot:
Email search / username / public profiles

Confidence:
Based on source and independent correlation
```

This makes the investigation reproducible.

---

# 30. My Actual Discovery Chain

This is the part I want people to pay attention to.

I started with:

```text
h4cker_fawad
```

Then:

```text
h4cker_fawad
↓
Open Profile
↓
Read Bio
↓
Find 5 Public Links
↓
Open Links
↓
Find GitHub
↓
Analyze Public GitHub Information
↓
Find Public Email
↓
cipherphantomofficial@gmail.com
```

So the email was **not the starting point**.

It was the result of following several public pivots.

---

# 31. Why This Is Better Than Running Random Tools

Someone can run ten OSINT tools and get hundreds of results.

That doesn't necessarily mean they have good intelligence.

My approach is:

```text
Find useful clue
↓
Understand it
↓
Follow it
↓
Find next clue
↓
Verify it
↓
Continue
```

This produces a much cleaner investigation.

---

# 32. Fact vs Inference

### Fact

```text
The h4cker_fawad profile contains public links.
```

### Fact

```text
One of those links leads to GitHub.
```

### Fact

```text
Public GitHub information revealed cipherphantomofficial@gmail.com.
```

### Inference

```text
Every account using a similar username must belong to the same person.
```

That last statement requires additional evidence.

I keep facts and assumptions separate.

---

# 33. Confidence

### Low

```text
One search result
```

### Medium

```text
Email
+
matching username
+
public profile
```

### High

```text
Email
+
public profile
+
GitHub
+
matching project
+
independent public source
```

The more independent evidence I have, the stronger the correlation.

---

# 34. My Practical Email OSINT Workflow

```text
1. Start with a public identifier
2. Inspect the profile manually
3. Read the bio
4. Follow public links
5. Identify useful platforms
6. Analyze public GitHub/GitLab information
7. Extract new identifiers
8. Search the discovered email
9. Search the email's local part
10. Search public documents
11. Check public websites
12. Check relevant OSINT tools
13. Find additional pivots
14. Correlate findings
15. Verify important findings
16. Record sources
17. Separate facts from assumptions
```

---

# 35. The Complete Pivot

My preferred way of thinking about email OSINT is:

```text
PUBLIC ACCOUNT
      ↓
BIO
      ↓
PUBLIC LINKS
      ↓
GITHUB
      ↓
PUBLIC PROJECT DATA
      ↓
EMAIL
      ↓
EMAIL SEARCH
      ↓
USERNAME / NAME / DOMAIN
      ↓
ADDITIONAL PUBLIC SOURCES
      ↓
CORRELATION
      ↓
VERIFICATION
      ↓
INTELLIGENCE
```

---

# 36. My Biggest Lesson

**Don't treat an email as the final result.**

Treat it as another door.

When I found:

```text
cipherphantomofficial@gmail.com
```

the investigation didn't end.

It created new pivots.

I can now ask:

```text
Where else is this email publicly mentioned?

Is the local part reused?

Is it connected to a public username?

Is it present in public Git history?

Is it connected to a project?

Is there a public website?

Are there independent sources confirming the connection?
```

That's where email OSINT becomes useful.

---

# 37. Final Rule

My rule is simple:

```text
Find
↓
Understand
↓
Pivot
↓
Correlate
↓
Verify
↓
Document
```

**One public account can lead to another platform.**

**Another platform can reveal another identifier.**

**That identifier can become the next pivot.**

That's how I discovered `cipherphantomofficial@gmail.com` from the public `h4cker_fawad` footprint — by following the publicly available links and analyzing the information they exposed, rather than guessing the email.
