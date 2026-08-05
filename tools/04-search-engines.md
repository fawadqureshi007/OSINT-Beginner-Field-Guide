
# 04 — Search Engines

## Why I Use Search Engines

After username enumeration, I don't stop at the tool results.

This is where I normally start doing the real manual work.

Search engines can connect things that a username tool doesn't understand as one identity.

A username can lead me to a name.

A name can lead me to an organization.

An organization can lead me to a website.

A website can lead me to documents, repositories, profiles and older pages.

So my mindset is:

**Don't search for the target once. Search every useful identifier you discover.**

---

# 1. Start With the Exact Username

If my starting point is:

```text
redteamerx
````

I first search it exactly:

```text
"redteamerx"
```

Then I remove the quotes and compare the results.

I also search the username with the platform:

```text
"redteamerx" Instagram
"redteamerx" GitHub
"redteamerx" LinkedIn
"redteamerx" Reddit
```

I record anything that looks useful.

I don't collect every random result.

---

# 2. Exclude the Original Platform

Sometimes the first platform dominates the search results.

If my original account is Instagram:

```text
"redteamerx" -instagram.com
```

Now I'm specifically looking for other indexed references.

This is one of the simplest searches, but it can save a lot of time.

---

# 3. Search a Username With Other Identifiers

Suppose the profile gives me a public name:

```text
Fawad Qureshi
```

Now I combine both identifiers:

```text
"Fawad Qureshi" "redteamerx"
```

Then I try related terms:

```text
"Fawad Qureshi" cybersecurity
"Fawad Qureshi" "offensive security"
"Fawad Qureshi" researcher
```

The important part is that I don't keep searching only the original username.

I search whatever new information I discover.

---

# 4. site: Operator

If I want results from one particular website, I use:

```text
site:github.com "redteamerx"
```

Examples:

```text
site:github.com "redteamerx"
site:linkedin.com "Fawad Qureshi"
site:reddit.com "redteamerx"
```

I can also combine identifiers:

```text
site:github.com "Fawad Qureshi" "redteamerx"
```

This is useful when a normal search produces too much noise.

---

# 5. filetype: Searches

If I'm looking for publicly indexed documents, I can search:

```text
"Fawad Qureshi" filetype:pdf
```

Other examples:

```text
"Fawad Qureshi" filetype:doc
"Fawad Qureshi" filetype:ppt
"redteamerx" filetype:pdf
```

I don't assume that finding a name inside a document means the document belongs to my target.

I inspect the actual document and its context.

---

# 6. Search Combinations

This is where search engines become much more useful.

Instead of:

```text
"Fawad Qureshi"
```

I build combinations:

```text
"Fawad Qureshi" cybersecurity
"Fawad Qureshi" Pakistan
"Fawad Qureshi" GitHub
"Fawad Qureshi" researcher
```

If I find a company:

```text
"Fawad Qureshi" "Company Name"
```

If I find a project:

```text
"Fawad Qureshi" "Project Name"
```

If I find another username:

```text
"redteamerx" "otherusername"
```

Every new identifier gives me another search.

---

# 7. Search The Bio

I don't ignore the bio.

A bio can contain:

* Another username
* Website
* Organization
* Job title
* Project
* Email
* Link
* Short phrase
* Brand name

For example, if a bio says:

```text
Offensive Security Researcher
```

I can search:

```text
"redteamerx" "Offensive Security Researcher"
```

If it contains another username:

```text
"redteamerx" "h4cker_fawad"
```

That can connect two public identities.

---

# 8. Search Profile Names

A display name can be more useful than a username.

If the profile shows:

```text
Fawad Qureshi
```

I search the exact name first:

```text
"Fawad Qureshi"
```

Then I add context:

```text
"Fawad Qureshi" cybersecurity
"Fawad Qureshi" Pakistan
"Fawad Qureshi" GitHub
```

The goal isn't to find every person with that name.

The goal is to separate the relevant results from unrelated people.

---

# 9. Search The Search Results Again

This is one of my biggest habits.

When I find a useful page, I don't just save the URL.

I extract new identifiers from it.

For example:

```text
Username
    ↓
GitHub profile
    ↓
Real/public name
    ↓
Repository
    ↓
Organization
    ↓
Website
```

Now I search the repository name.

Then the organization.

Then the website.

Then any other public identifier that looks relevant.

This is how I keep expanding the investigation.

---

# 10. Don't Search Everything at Once

A common mistake is making one giant search query.

I prefer small controlled searches.

For example:

```text
"redteamerx"
```

Then:

```text
"redteamerx" GitHub
```

Then:

```text
"Fawad Qureshi" "redteamerx"
```

Then:

```text
site:github.com "Fawad Qureshi"
```

Each search answers a different question.

---

# 11. Search Old Information

I also search combinations that may expose older indexed pages.

Examples:

```text
"redteamerx" old
"redteamerx" archive
"redteamerx" forum
"redteamerx" blog
```

If I discover an old username:

```text
"oldusername"
```

Then I connect it back to the other identifiers.

Historical information can sometimes explain relationships that aren't visible on a current profile.

---

# 12. Search Public Technical Information

If the target publicly identifies a domain, project or organization, I pivot into technical OSINT.

For example:

```text
"example.com"
```

Then:

```text
site:github.com "example.com"
```

or:

```text
"example.com" "GitHub"
```

The purpose here is not to attack anything.

I'm looking for publicly indexed information and relationships.

---

# 13. Search Engines Are Also Verification Tools

I don't use search engines only to discover information.

I use them to verify information from other tools.

If Maigret gives me:

```text
redteamerx → Website X
```

I search:

```text
"redteamerx" "Website X"
```

If Sherlock gives me a possible GitHub account:

```text
site:github.com "redteamerx"
```

If a reverse-image search gives me a name:

```text
"Name" "redteamerx"
```

Independent searches can help determine whether a result is actually connected or just noise.

---

# 14. My Search Notes

For useful discoveries I record:

```text
Query:
URL:
Finding:
New identifier:
Source:
Fact or inference:
Confidence:
```

Example:

```text
Query:
"redteamerx" GitHub

Finding:
A public GitHub profile using the same username.

New identifier:
GitHub username

Confidence:
Low
```

Then I investigate the account instead of immediately calling it the target.

---

# 15. My Search Mindset

I don't think:

> What information can Google give me?

I think:

> What identifier can I extract from this result?

That difference completely changes the investigation.

A search result might give me:

```text
Name
```

The name becomes a new search.

That search might give me:

```text
Organization
```

The organization becomes another search.

That might give me:

```text
Website
```

The website becomes another pivot.

---

# 16. My Manual Workflow

```text
Starting username
        ↓
Exact search
        ↓
Remove original platform
        ↓
Search username variations
        ↓
Search discovered name
        ↓
Search discovered usernames
        ↓
site: searches
        ↓
filetype: searches
        ↓
Search organizations/projects
        ↓
Search technical identifiers
        ↓
Cross-check results
        ↓
Document evidence
```

---

# 17. The Rule I Follow

I never treat search-engine ranking as evidence.

Just because something appears at the top doesn't mean it is the correct person.

I check:

**Who published it?**

**When was it published?**

**What identifiers match?**

**Is there independent evidence?**

**Could this belong to another person?**

If I can't answer those questions, I keep the finding as a lead.

---

# Final Point

Search engines are not just a place where I type a name.

For me, they are a manual pivot system.

One search gives me an identifier.

That identifier gives me another search.

Another search gives me another connection.

The investigation grows from those connections.

**Search → Extract → Pivot → Correlate → Verify → Document.**

