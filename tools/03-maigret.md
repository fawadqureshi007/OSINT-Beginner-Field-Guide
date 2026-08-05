
# 03 — Maigret

## What is Maigret?

Maigret is another username OSINT tool I use to search for a username across many public websites.

My main reason for using it is simple:

I already have a username, and I want to discover where that same username appears publicly.

But the same rule applies here:

**A username match is a lead, not proof of identity.**

---

## 1. Install Maigret

Clone the repository:

```bash
git clone https://github.com/soxoj/maigret.git
````

Move into the directory:

```bash
cd maigret
```

Install the requirements:

```bash
python3 -m pip install -r requirements.txt
```

Check the help menu:

```bash
python3 -m maigret --help
```

If the help menu appears, Maigret is ready.

---

## 2. Basic Search

The basic command is:

```bash
python3 -m maigret USERNAME
```

Example:

```bash
python3 -m maigret redteamerx
```

Maigret will search its supported sites and return possible matches.

---

## 3. What I Do With the Results

I don't just copy the output and call it intelligence.

I open the interesting results manually.

For every possible match I check:

* Username
* Display name
* Profile picture
* Bio
* Website
* Public location
* Organization
* Public activity
* Posts
* Projects
* Account history
* Links to other public accounts

I'm looking for **correlation**, not just matching text.

---

## 4. Example

Suppose Maigret gives me:

```text
redteamerx → Website A
redteamerx → Website B
redteamerx → Website C
```

I treat these as three leads.

Then I investigate them separately.

If Website A has:

```text
Username: redteamerx
Name: Same public name
Website: Same domain
```

that becomes a stronger correlation.

If Website B only has:

```text
Username: redteamerx
```

I keep it as an unconfirmed match.

---

## 5. Search the New Information

The interesting part starts when Maigret gives me something new.

For example, if I discover a public name:

```text
"Full Name" "redteamerx"
```

If I discover an organization:

```text
"Full Name" "Organization"
```

If I discover a project:

```text
"redteamerx" "Project Name"
```

I search those identifiers separately.

One discovery can create another pivot.

---

## 6. My Verification Method

My basic verification chain is:

```text
Username
   ↓
Maigret result
   ↓
Open the account
   ↓
Compare identifiers
   ↓
Find another identifier
   ↓
Search that identifier
   ↓
Find independent evidence
   ↓
Correlate
   ↓
Assign confidence
```

I don't force a connection just because I want the investigation to continue.

If the evidence doesn't connect, I mark it as unconfirmed and move on.

---

## 7. Username vs Identity

This is probably the most important thing to understand.

```text
Same username ≠ Same person
```

A username can be:

* Reused
* Impersonated
* Abandoned
* Registered by another person
* Used by different people on different platforms

So I separate my notes into:

### Confirmed

Information supported by strong evidence.

### Possible

A reasonable connection but not enough independent evidence.

### Unconfirmed

Only a username or weak indicator matches.

This keeps the investigation clean.

---

## 8. Maigret vs Sherlock

I don't treat one tool as automatically better.

I use them for slightly different purposes.

| Tool                 | My Use                        |
| -------------------- | ----------------------------- |
| Sherlock             | Quick username enumeration    |
| Maigret              | Deeper username investigation |
| Search engines       | Context and additional pivots |
| Manual browsing      | Verification                  |
| Reverse-image search | Image correlation             |

My normal workflow can therefore be:

```text
Manual search
      ↓
Sherlock
      ↓
Maigret
      ↓
Compare results
      ↓
Remove obvious false positives
      ↓
Investigate interesting matches
```

If both tools report the same public account, that can make the account more interesting to investigate.

But even then:

**Two tools agreeing does not automatically prove identity.**

They may both be detecting the same username.

---

## 9. What I Like About Maigret

The biggest value for me is the amount of information it can help me discover around a username.

Instead of manually starting from zero, I get a list of possible places to investigate.

That saves time.

But I still do the important part manually.

---

## 10. What I Don't Like

The number of results can sometimes create false confidence.

Seeing a large result count looks impressive, but the number itself isn't intelligence.

For me:

```text
100 weak matches
```

can be less useful than:

```text
2 strong, independently verified matches
```

Quality of correlation matters more than quantity.

---

## 11. My Practical Rule

When Maigret finishes, I don't ask:

> How many accounts did I find?

I ask:

> Which result gives me the strongest new pivot?

That pivot might be:

* A public name
* Another username
* A website
* An organization
* A project
* A public profile
* A public document

Then I continue from there.

---

## 12. Evidence Notes

For useful results I record:

```text
Username:
Platform:
URL:
Display name:
Profile image:
Bio:
Other identifier:
Why it may be connected:
Confidence:
```

I also keep **fact** and **inference** separate.

Example:

```text
Fact:
The account uses the username redteamerx.

Inference:
The account may belong to the same person as the original profile.
```

Those are not the same thing.

---

## Final Takeaway

Maigret helps me discover possible username reuse.

It does not perform the entire investigation for me.

My actual process is:

```text
Find
→ Compare
→ Correlate
→ Verify
→ Document
```

The tool gives me leads.

The investigation comes from what I do with those leads.

```

**Next file:** `04-search-engines.md` — this is where we can cover Google/Bing operators, exact searches, `site:`, `filetype:`, exclusions, combining identifiers, and your manual-search methodology.
```
Bro, for **`03-maigret.md`**, paste this:

````markdown
# 03 — Maigret

## What is Maigret?

Maigret is another username OSINT tool I use to search for a username across many public websites.

My main reason for using it is simple:

I already have a username, and I want to discover where that same username appears publicly.

But the same rule applies here:

**A username match is a lead, not proof of identity.**

---

## 1. Install Maigret

Clone the repository:

```bash
git clone https://github.com/soxoj/maigret.git
````

Move into the directory:

```bash
cd maigret
```

Install the requirements:

```bash
python3 -m pip install -r requirements.txt
```

Check the help menu:

```bash
python3 -m maigret --help
```

If the help menu appears, Maigret is ready.

---

## 2. Basic Search

The basic command is:

```bash
python3 -m maigret USERNAME
```

Example:

```bash
python3 -m maigret redteamerx
```

Maigret will search its supported sites and return possible matches.

---

## 3. What I Do With the Results

I don't just copy the output and call it intelligence.

I open the interesting results manually.

For every possible match I check:

* Username
* Display name
* Profile picture
* Bio
* Website
* Public location
* Organization
* Public activity
* Posts
* Projects
* Account history
* Links to other public accounts

I'm looking for **correlation**, not just matching text.

---

## 4. Example

Suppose Maigret gives me:

```text
redteamerx → Website A
redteamerx → Website B
redteamerx → Website C
```

I treat these as three leads.

Then I investigate them separately.

If Website A has:

```text
Username: redteamerx
Name: Same public name
Website: Same domain
```

that becomes a stronger correlation.

If Website B only has:

```text
Username: redteamerx
```

I keep it as an unconfirmed match.

---

## 5. Search the New Information

The interesting part starts when Maigret gives me something new.

For example, if I discover a public name:

```text
"Full Name" "redteamerx"
```

If I discover an organization:

```text
"Full Name" "Organization"
```

If I discover a project:

```text
"redteamerx" "Project Name"
```

I search those identifiers separately.

One discovery can create another pivot.

---

## 6. My Verification Method

My basic verification chain is:

```text
Username
   ↓
Maigret result
   ↓
Open the account
   ↓
Compare identifiers
   ↓
Find another identifier
   ↓
Search that identifier
   ↓
Find independent evidence
   ↓
Correlate
   ↓
Assign confidence
```

I don't force a connection just because I want the investigation to continue.

If the evidence doesn't connect, I mark it as unconfirmed and move on.

---

## 7. Username vs Identity

This is probably the most important thing to understand.

```text
Same username ≠ Same person
```

A username can be:

* Reused
* Impersonated
* Abandoned
* Registered by another person
* Used by different people on different platforms

So I separate my notes into:

### Confirmed

Information supported by strong evidence.

### Possible

A reasonable connection but not enough independent evidence.

### Unconfirmed

Only a username or weak indicator matches.

This keeps the investigation clean.

---

## 8. Maigret vs Sherlock

I don't treat one tool as automatically better.

I use them for slightly different purposes.

| Tool                 | My Use                        |
| -------------------- | ----------------------------- |
| Sherlock             | Quick username enumeration    |
| Maigret              | Deeper username investigation |
| Search engines       | Context and additional pivots |
| Manual browsing      | Verification                  |
| Reverse-image search | Image correlation             |

My normal workflow can therefore be:

```text
Manual search
      ↓
Sherlock
      ↓
Maigret
      ↓
Compare results
      ↓
Remove obvious false positives
      ↓
Investigate interesting matches
```

If both tools report the same public account, that can make the account more interesting to investigate.

But even then:

**Two tools agreeing does not automatically prove identity.**

They may both be detecting the same username.

---

## 9. What I Like About Maigret

The biggest value for me is the amount of information it can help me discover around a username.

Instead of manually starting from zero, I get a list of possible places to investigate.

That saves time.

But I still do the important part manually.

---

## 10. What I Don't Like

The number of results can sometimes create false confidence.

Seeing a large result count looks impressive, but the number itself isn't intelligence.

For me:

```text
100 weak matches
```

can be less useful than:

```text
2 strong, independently verified matches
```

Quality of correlation matters more than quantity.

---

## 11. My Practical Rule

When Maigret finishes, I don't ask:

> How many accounts did I find?

I ask:

> Which result gives me the strongest new pivot?

That pivot might be:

* A public name
* Another username
* A website
* An organization
* A project
* A public profile
* A public document

Then I continue from there.

---

## 12. Evidence Notes

For useful results I record:

```text
Username:
Platform:
URL:
Display name:
Profile image:
Bio:
Other identifier:
Why it may be connected:
Confidence:
```

I also keep **fact** and **inference** separate.

Example:

```text
Fact:
The account uses the username redteamerx.

Inference:
The account may belong to the same person as the original profile.
```

Those are not the same thing.

---

## Final Takeaway

Maigret helps me discover possible username reuse.

It does not perform the entire investigation for me.

My actual process is:

```text
Find
→ Compare
→ Correlate
→ Verify
→ Document
```

The tool gives me leads.

The investigation comes from what I do with those leads.

