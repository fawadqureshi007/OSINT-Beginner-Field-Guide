
# 02 — Sherlock

## What is Sherlock?

Sherlock is one of the tools I use for username enumeration.

I give it a username and it checks that username across many supported websites.

For me, Sherlock is mainly a **lead-generation tool**.

It helps me answer:

> Where else does this username appear publicly?

It does NOT automatically answer:

> Do all these accounts belong to the same person?

That second part is my job.

---

## 1. Install Sherlock

First clone the repository:

```bash
git clone https://github.com/sherlock-project/sherlock.git
````

Move into the directory:

```bash
cd sherlock
```

Install the requirements:

```bash
python3 -m pip install -r requirements.txt
```

Check that Sherlock starts:

```bash
python3 sherlock --help
```

If the help menu appears, the installation is working.

---

## 2. Basic Username Search

The basic command is:

```bash
python3 sherlock USERNAME
```

For my self-OSINT test:

```bash
python3 sherlock redteamerx
```

Sherlock will check the username against its supported sites and display possible matches.

---

## 3. Don't Trust the Results Blindly

This is the part I care about most.

If Sherlock gives me:

```text
redteamerx → GitHub
redteamerx → Reddit
redteamerx → X
```

I don't immediately say:

> I found the target on three platforms.

I say:

> I found three possible username matches.

Then I manually open them.

---

## 4. What I Check Manually

For every interesting result, I compare:

* Username
* Display name
* Profile picture
* Bio
* Website
* Public location
* Organization
* Public interests
* Posts
* Projects
* Account history
* Links to other accounts

I want more than one matching identifier.

For example:

```text
Same username
+
Same profile image
+
Same public name
+
Same website
```

is much more useful than:

```text
Same username
```

---

## 5. Search Engine Verification

After Sherlock gives me an interesting result, I search for that username manually.

Example:

```text
"redteamerx" "github"
```

Then:

```text
"redteamerx" -instagram.com
```

If I discover a public name:

```text
"Full Name" "redteamerx"
```

If I discover an organization:

```text
"Full Name" "Organization"
```

Every useful discovery can become another pivot.

---

## 6. What Sherlock Is Good At

I mainly use Sherlock for:

### Fast enumeration

Instead of manually checking dozens of websites one by one, Sherlock can quickly give me possible places where the username appears.

### Initial reconnaissance

It gives me a starting list of accounts that I can investigate manually.

### Finding unexpected platforms

Sometimes a username appears somewhere I wasn't thinking about.

That can create a completely new pivot.

---

## 7. What Sherlock Is NOT Good At

Sherlock does not prove identity.

A username can be reused by different people.

For example:

```text
Person A → redteamerx → Instagram

Person B → redteamerx → Reddit
```

Sherlock can find both.

It cannot know from the username alone that they are the same person.

That's why I always verify the result manually.

---

## 8. My Verification Flow

```text
Username
   ↓
Sherlock
   ↓
Possible matches
   ↓
Open interesting results
   ↓
Compare profile information
   ↓
Find additional identifiers
   ↓
Search those identifiers
   ↓
Correlate independent evidence
   ↓
Assign confidence
```

---

## 9. My Point of View

I don't consider Sherlock the final tool.

I consider it the **first filter**.

It saves time by giving me possible places to investigate.

The real OSINT work starts after Sherlock finishes.

A tool can tell me:

```text
username exists here
```

My investigation has to determine:

```text
why this account may or may not be connected
```

That's a very different thing.

---

## 10. Common Beginner Mistake

Don't write:

```text
Sherlock found 40 accounts.
```

and then conclude:

```text
The target has 40 social-media accounts.
```

That's wrong.

The correct conclusion is:

```text
Sherlock found 40 possible username matches.
```

Then I investigate the useful ones.

---

## 11. My Practical Rule

I use Sherlock when I want **speed**.

I use manual searching when I want **context**.

I use correlation when I want **confidence**.

My workflow is therefore:

```text
Sherlock
+
Search engines
+
Manual verification
+
Independent evidence
```

No single Sherlock result should become an identity claim by itself.

---

## Final Takeaway

Sherlock is excellent for answering:

> "Where should I look next?"

It is not an identity-verification system.

For me, the value of Sherlock is not the number of results.

The value is whether one of those results gives me a **useful new pivot**.

