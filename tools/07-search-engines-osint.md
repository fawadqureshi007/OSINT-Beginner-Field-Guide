

# 07 — Search Engine OSINT

## My Approach

Search engines are one of the simplest OSINT tools, but people usually use them badly.

They search the target's name once, look at the first few results and stop.

I don't work like that.

I take every useful identifier I discover and turn it into a new search.

A username can lead to a profile.

A profile can reveal a name.

A name can reveal an organization.

An organization can reveal a website.

A website can reveal documents, projects, employees and other public information.

For me, search-engine OSINT is basically:

**Identifier → Query → Result → Pivot → Verification**

---

## 1. Start With Exact Searches

If I have a username:

```text
"redteamerx"
```

I start with the exact phrase.

Then I try:

```text
"redteamerx" Instagram
```

```text
"redteamerx" GitHub
```

```text
"redteamerx" LinkedIn
```

```text
"redteamerx" cybersecurity
```

The quotation marks matter because I want the search engine to look for that exact phrase.

---

## 2. Search Without the Original Platform

If Instagram is already known, I don't want every result to be Instagram.

I can remove it:

```text
"redteamerx" -instagram.com
```

Or:

```text
"redteamerx" -instagram
```

This can expose other public pages using the same identifier.

But I still verify whether those pages belong to the same person.

---

## 3. Search the Public Name

If the profile gives me a name:

```text
"Fawad Qureshi"
```

Then I combine it with useful context:

```text
"Fawad Qureshi" cybersecurity
```

```text
"Fawad Qureshi" "offensive security"
```

```text
"Fawad Qureshi" GitHub
```

```text
"Fawad Qureshi" Pakistan
```

The idea is to reduce irrelevant results.

A common name can produce hundreds of unrelated people.

---

# 4. `site:` Operator

One of my most useful operators is:

```text
site:
```

For example:

```text
"redteamerx" site:github.com
```

```text
"redteamerx" site:linkedin.com
```

```text
"redteamerx" site:reddit.com
```

```text
"redteamerx" site:medium.com
```

This tells the search engine to focus on a particular website.

---

## 5. Search Specific Platforms

If I suspect a username exists somewhere:

```text
site:github.com "redteamerx"
```

```text
site:linkedin.com "Fawad Qureshi"
```

```text
site:medium.com "Fawad Qureshi"
```

```text
site:youtube.com "redteamerx"
```

```text
site:x.com "redteamerx"
```

I don't consider a search result proof of ownership.

It is only a possible match.

---

# 6. `filetype:` Operator

Public documents can contain useful information.

I can search:

```text
"Fawad Qureshi" filetype:pdf
```

```text
"Fawad Qureshi" filetype:doc
```

```text
"Fawad Qureshi" filetype:ppt
```

I can also combine it with an organization:

```text
"Fawad Qureshi" "Company Name" filetype:pdf
```

The important part is that I only use publicly accessible documents.

I don't try to access restricted files.

---

# 7. `intitle:` Operator

This searches for a phrase in the page title.

Example:

```text
intitle:"Fawad Qureshi"
```

Or:

```text
intitle:"redteamerx"
```

I can combine it with other terms:

```text
intitle:"Fawad Qureshi" cybersecurity
```

This can sometimes find pages that don't appear in normal searches.

---

# 8. `inurl:` Operator

This looks for a term inside a URL.

For example:

```text
inurl:redteamerx
```

Or:

```text
site:github.com inurl:redteamerx
```

This can be useful when usernames or identifiers are included directly in URLs.

---

# 9. Combine Operators

The real value comes from combining them.

For example:

```text
site:github.com "redteamerx" cybersecurity
```

Or:

```text
site:linkedin.com "Fawad Qureshi" "offensive security"
```

Or:

```text
"Fawad Qureshi" filetype:pdf cybersecurity
```

The more specific the query, the less irrelevant information I usually get.

---

# 10. Search Different Username Variations

People don't always use one exact username everywhere.

If the target is:

```text
redteamerx
```

I may test public variations such as:

```text
redteamerx
redteamer_x
redteamer-x
redteamerx01
h4cker_fawad
```

I only investigate variations that are reasonably derived from information already publicly associated with the target.

I don't randomly generate hundreds of usernames and treat every result as belonging to the target.

---

# 11. Search the Bio

A bio can contain better search terms than the username.

Suppose the bio says:

```text
Offensive Security Researcher
```

I can search:

```text
"redteamerx" "Offensive Security Researcher"
```

Or:

```text
"Fawad Qureshi" "Offensive Security Researcher"
```

This combines two identifiers.

That is usually stronger than searching the name alone.

---

# 12. Search Public Links

If the profile contains:

```text
example.com
```

I investigate the domain separately.

I search:

```text
"example.com"
```

Then:

```text
site:example.com
```

Then I look for publicly available:

* About pages
* Team pages
* Blog posts
* Projects
* Public documents
* Contact pages
* Author pages

The domain becomes a new pivot.

---

# 13. Search Project Names

Suppose I discover a public project called:

```text
BlackTrace
```

I don't stop at the original profile.

I search:

```text
"BlackTrace"
```

Then:

```text
"BlackTrace" GitHub
```

Then:

```text
"BlackTrace" cybersecurity
```

Then:

```text
"BlackTrace" "Fawad Qureshi"
```

A project name can connect multiple public sources.

---

# 14. Search Organizations

If I discover an organization:

```text
"Organization Name"
```

Then I search:

```text
"Organization Name" employees
```

```text
"Organization Name" events
```

```text
"Organization Name" cybersecurity
```

```text
"Organization Name" "Fawad Qureshi"
```

I use the organization only as a pivot.

I don't assume that appearing on an organization's website means employment.

---

# 15. Search Public Documents

When a useful public identifier appears in a document, I search that identifier separately.

For example:

```text
"Project Name" filetype:pdf
```

```text
"Project Name" filetype:ppt
```

```text
"Organization Name" filetype:pdf
```

Documents can reveal public:

* Project names
* Event participation
* Publications
* Presentations
* Public affiliations
* Technical information

I verify the document source and date before using it.

---

# 16. Search Old Information

Search engines can sometimes expose older public pages.

I search:

```text
"oldusername"
```

```text
"oldusername" "newusername"
```

```text
"oldusername" cybersecurity
```

If I find an old page, I compare:

* Username
* Name
* Profile image
* Bio
* Website
* Dates
* Public projects

One matching identifier isn't enough.

---

# 17. Search Engines Can Find Forgotten Pages

Sometimes people forget that information was publicly indexed.

For example:

```text
"username"
```

may reveal:

* Old profiles
* Blog posts
* Public comments
* Project pages
* Cached references
* Public documents
* Event pages

But an indexed page is not automatically current.

I always check the date and context.

---

# 18. Search By Unique Phrases

Sometimes the best identifier isn't a username.

It can be a sentence from a public bio, article or project description.

For example:

```text
"Building a life I'm proud of"
```

Then I combine it:

```text
"Building a life I'm proud of" cybersecurity
```

Unique phrases can sometimes locate copies of the same public profile or text.

---

# 19. Search Public Email Addresses

If an email address is already publicly displayed by the target or an organization, I can search the exact address:

```text
"example@example.com"
```

Then combine it with public context:

```text
"example@example.com" GitHub
```

```text
"example@example.com" website
```

I only use contact information that is already publicly available.

I don't attempt to obtain private email addresses.

---

# 20. Search Phone Numbers Carefully

If a phone number is legitimately published on a public business page, I can search the exact number.

Example:

```text
"+92XXXXXXXXXX"
```

But I don't use search engines to hunt for private contact information.

The goal is public-source research, not discovering information that someone intentionally kept private.

---

# 21. Search Images Through Text

Sometimes I find a screenshot containing:

```text
username
website
event
company
location
```

I extract the text and search it separately.

For example:

```text
"event name" "company name"
```

This can reveal the original public page.

---

# 22. Search by Date

Dates can make a search much more precise.

For example:

```text
"Fawad Qureshi" cybersecurity 2025
```

Or:

```text
"redteamerx" 2024
```

I can then compare the result with the target's known public timeline.

---

# 23. Search Public Events

If the target mentions an event:

```text
"Event Name" "Fawad Qureshi"
```

Then:

```text
"Event Name" cybersecurity
```

I look for public:

* Event pages
* Speaker lists
* Photos
* Videos
* Announcements
* Organization pages

An event can provide several independent public sources.

---

# 24. Search Engines + Reverse Image Search

These two methods work well together.

For example:

Image → Google Lens → Event page

Then:

```text
"Event Name" "Fawad Qureshi"
```

Now the image result and text search can be compared.

This is much stronger than relying on the visual result alone.

---

# 25. Search Engines + Social Media

Example:

```text
Instagram username
↓
Search engine
↓
GitHub result
↓
GitHub username
↓
Public repository
↓
Project name
↓
Website
```

The search engine is acting as the bridge between public sources.

---

# 26. My Query Ladder

I normally start broad and become more specific.

### Level 1

```text
"redteamerx"
```

### Level 2

```text
"redteamerx" cybersecurity
```

### Level 3

```text
"redteamerx" "Fawad Qureshi"
```

### Level 4

```text
site:github.com "redteamerx"
```

### Level 5

```text
site:github.com "Fawad Qureshi" cybersecurity
```

### Level 6

```text
"Fawad Qureshi" filetype:pdf cybersecurity
```

Each new discovery can create another query.

---

# 27. Don't Search Randomly

I keep a search log.

| Query                           | Result           | New Identifier  | Confidence |
| ------------------------------- | ---------------- | --------------- | ---------- |
| `"redteamerx"`                  | Public profile   | Fawad Qureshi   | High       |
| `"redteamerx" GitHub`           | Possible profile | GitHub username | Low        |
| `"Fawad Qureshi" cybersecurity` | Public article   | Article         | Medium     |

This prevents me from forgetting where a finding came from.

---

# 28. Verify Search Results

This is extremely important.

Search engines sometimes return:

* Same names
* Similar usernames
* Scraped pages
* Old information
* Incorrect associations
* Automatically generated pages

I open the actual source.

Then I compare the identifiers.

For example:

**Same username**

→ possible

**Same username + same public name**

→ stronger

**Same username + same name + same project**

→ stronger again

**Same username + same name + linked public profile**

→ much stronger

---

# 29. Search Result Is Not Evidence by Itself

I don't write:

> Google says this is the target.

I write:

> The search result led to this public page, where these identifiers were independently observed.

That difference matters.

The search engine is helping me locate the source.

The source itself is what I evaluate.

---

# 30. Search Result Confidence

I use:

### Low

One matching identifier.

### Medium

Multiple matching identifiers but no strong independent connection.

### High

Several independent public sources support the same connection.

I also record conflicting information instead of ignoring it.

---

# 31. My Favorite Search-Engine Pivots

The most useful pivots I've found are usually:

* Username
* Full name
* Previous username
* Unique phrase
* Project name
* Organization
* Website
* Public email
* Event name
* Public document title

The important thing is not how many queries I run.

It's how many useful pivots I discover.

---

# 32. What I Don't Do

I don't:

* Treat search results as proof
* Assume identical names are the same person
* Assume identical usernames belong to one person
* Search for private information
* Bypass authentication
* Access restricted documents
* Use leaked credentials
* Ignore contradictory evidence
* Publish unnecessary personal information

I stay within publicly accessible information and verify what I find.

---

# 33. My Practical Workflow

```text
Target
  ↓
Collect identifiers
  ↓
Exact username search
  ↓
Search name
  ↓
Search username variations
  ↓
Use site:
  ↓
Search unique phrases
  ↓
Search organizations
  ↓
Search projects
  ↓
Search public documents
  ↓
Search historical identifiers
  ↓
Find new public pivots
  ↓
Open original sources
  ↓
Correlate
  ↓
Verify
  ↓
Document
```

---

# My Point of View

Search engines are probably the most underestimated OSINT tool.

You don't need a huge framework to start.

Sometimes one carefully constructed query gives me something more useful than running ten automated tools.

But the important part is knowing what to search next.

If I find:

```text
Username
```

I search it.

If I find:

```text
Name
```

I search it.

If I find:

```text
Project
```

I search it.

If I find:

```text
Organization
```

I search it.

If I find:

```text
Website
```

I search it.

Every useful discovery becomes another pivot.

That's the mindset I want beginners to understand.

**Don't just search the target. Search the identifiers you discover around the target.**

---

# Final Rule

**A search engine is not an intelligence source by itself. It is a discovery layer.**

Use it to locate public information.

Open the original source.

Check the context.

Correlate identifiers.

Verify independently.

Then document the finding.

**Search → Discover → Pivot → Correlate → Verify → Document**
