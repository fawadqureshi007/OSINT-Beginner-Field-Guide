
# 05 — Social Media OSINT

## My Approach

After username enumeration and search-engine work, I move back to the actual social-media profile.

This is where I stop looking at the target as just one account.

I look at the public network around that account.

The target is one point. Followers, following, comments, tags, mentions, public posts, projects, organizations and connected accounts can become other points.

The useful information is often in the connections between them.

My mindset is simple:

**Don't just ask what the target posted. Ask what the target's public network reveals.**

---

## 1. Start With the Target

First I collect the information that is already publicly visible.

I check:

* Username
* Display name
* Bio
* Profile picture
* Public links
* Public posts
* Highlights
* Mentions
* Tags
* Followers
* Following
* Public professional information
* Public organizations
* Other usernames

I don't make a conclusion at this stage.

I just build my starting point.

---

## 2. Build an Identifier List

I turn everything useful from the profile into identifiers.

For example:

**Username:** `redteamerx`

**Name:** `Fawad Qureshi`

**Other username:** `h4cker_fawad`

**Public role:** `Offensive Security Researcher`

Now I have several things that I can search and correlate instead of relying on one username.

This is important because usernames can be reused and accounts can change their usernames.

---

## 3. Check Followers

I don't look at the follower count and move on.

I look through the public follower list for useful patterns.

Things I pay attention to:

* People repeatedly interacting with the target
* Same organization
* Same university
* Same workplace
* Project members
* Professional accounts
* Community accounts
* Event accounts
* Publicly stated relationships
* Accounts that repeatedly appear around the target

One follower by itself usually doesn't tell me much.

Repeated public connections are more interesting.

---

## 4. Check Following

I also check who the target follows.

Sometimes the following list gives me more context than the target's own bio.

I look for:

* Companies
* Universities
* Security organizations
* Communities
* Events
* Professional accounts
* Project accounts
* Friends
* Public creators
* Related usernames

For example:

Target → follows organization → organization profile → public event → event page

I don't automatically assume the target works for or belongs to that organization.

It is only a lead until I verify it.

---

## 5. Look for Repeated Accounts

This is one of the things I pay close attention to.

If the same account appears in:

* Followers
* Following
* Comments
* Mentions
* Tags
* Public posts

I mark that account for further investigation.

I don't immediately write:

> "This is the target's friend."

I write:

> "This account has repeated public association with the target."

Then I investigate why.

---

## 6. Interaction Patterns

One interaction is weak.

Repeated public interaction is more interesting.

For example:

Target post → Account A comments

Target post → Account A appears again

Target post → Account A is tagged

Target → Account A follows each other

Now I have a stronger reason to investigate Account A.

But repeated interaction still doesn't automatically prove a private relationship.

It is evidence of public interaction, not proof of friendship.

---

## 7. Comments

Comments can give me identifiers that aren't visible anywhere else on the profile.

I look for:

* Names
* Nicknames
* Usernames
* Organizations
* Events
* Projects
* Public locations
* Websites
* Context about the post

For example:

Target post → public comment → new username → new public profile

That new username becomes another pivot.

---

## 8. Mentions

I check who publicly mentions the target.

Then I look at the context.

Why was the target mentioned?

It could be:

* An event
* A project
* A collaboration
* A public achievement
* A community activity
* A professional connection

The mention itself isn't always useful.

The surrounding context is what matters.

---

## 9. Tagged Posts

Public tagged posts can be useful because they sometimes contain information the target didn't publish themselves.

I check:

* Who uploaded it
* Date
* Caption
* Other people
* Event
* Organization
* Public location
* Visible signs
* Comments
* Related posts

One tagged photo might create several new pivots.

---

## 10. Public Highlights

If highlights are public, I go through them carefully.

I look for:

* Events
* Education
* Work
* Projects
* Travel
* Conferences
* Public gatherings
* Organizations
* Public locations
* Repeated people

I also look at older content.

Sometimes an old public post contains an identifier that no longer appears on the current profile.

---

## 11. Background Information

Sometimes the person isn't the most useful part of the image.

The background can contain:

* Road signs
* Building names
* University names
* Company signs
* Event banners
* Restaurant names
* Public landmarks
* Venue names
* Logos
* Public transportation information

For example, a person may upload a normal event photograph.

The caption says nothing about the location.

But the background may contain the name of the venue.

That venue becomes a new search pivot.

I don't treat one visual clue as final proof.

I verify it with other public information.

---

## 12. Reverse Image Search

When a publicly available image looks useful, I can test it with:

* Google Lens
* Bing Visual Search
* Yandex Images
* TinEye

I look for:

* Older appearances
* Other public profiles
* Websites
* Articles
* Public project pages
* Reposted versions

A match is still only a lead.

The same image can be copied by completely unrelated accounts.

---

## 13. Profile Picture Correlation

A profile picture can sometimes connect accounts with different usernames.

I compare:

* Same image
* Cropped version
* Older version
* Same branding
* Same public visual identity

But I don't say two accounts belong to the same person just because their profile pictures look similar.

I want another identifier to support the connection.

---

## 14. Public Relationships

If someone publicly identifies another person as a:

* Friend
* Brother
* Sister
* Colleague
* Classmate
* Teammate
* Project partner

I can record that public statement as a lead.

I don't guess private relationships from photographs or appearances.

For example:

Target → publicly identified colleague → colleague profile → organization → public website

The second account may provide a completely new public pivot.

---

## 15. Investigate Interesting Accounts

If I find an account that repeatedly appears around the target, I investigate that account separately.

I check:

* Username
* Name
* Bio
* Profile picture
* Website
* Organization
* Public posts
* Public links
* Other public accounts

Then I ask:

**Does this account give me another useful identifier?**

If yes, I follow that pivot.

---

## 16. Think in a Social Graph

I think about social media like a graph:

Target → Account A → Organization → Event → Website

Or:

Target → Account B → Project → GitHub → Public repository

Or:

Target → Public post → Venue → Event page → Other public accounts

The target is only the starting point.

The investigation expands through public connections.

---

## 17. Don't Investigate Every Account

This is where I try to avoid wasting time.

I don't need to investigate hundreds of random followers.

I prioritize accounts that have:

1. Repeated interaction
2. Shared public identifiers
3. Relevant organizations
4. Public professional connections
5. Shared projects
6. Useful websites
7. Strong contextual connections

The goal isn't to collect the maximum amount of data.

The goal is to find the **useful data**.

---

## 18. Cross-Platform Correlation

If I find another public account, I compare:

* Username
* Name
* Profile image
* Bio
* Website
* Organization
* Projects
* Public links
* Other identifiers

For example:

Instagram → username → GitHub → repository → project → website

Every connection needs to make sense.

---

## 19. Search New Identifiers

This is one of the most important parts.

I don't keep searching the original username forever.

If I discover a project called:

`Project X`

I search:

`"Project X"`

If I discover an organization:

`Organization Y`

I search:

`"Organization Y"`

If I discover an older username:

`oldusername`

I search:

`"oldusername"`

Every useful discovery can become a new pivot.

---

## 20. Historical Information

I also pay attention to older public information.

For example:

2023 → Old username

2024 → Different public profile

2025 → New project

2026 → Current account

An old username or old project can sometimes connect current and historical public information.

But I still verify that the old account actually belongs to the same person.

---

## 21. Evidence Matters

For important findings, I record:

**Target**

**Connected account**

**Platform**

**URL**

**What I observed**

**New identifier**

**Evidence**

**Fact or inference**

**Confidence**

For example:

Target: `redteamerx`

Connected account: `example_account`

Observation: Repeated public interaction

Evidence: Public comments and tagged content

Assessment: Possible connection

Confidence: Medium

---

## 22. Fact vs Inference

I keep these completely separate.

### Fact

Account A publicly commented on the target's post.

### Inference

Account A probably knows the target.

The first one is directly observable.

The second one is my interpretation.

I don't turn the interpretation into a confirmed fact.

---

## 23. Confidence

I normally think about findings as:

### High

Several independent public sources support the same conclusion.

### Medium

There are multiple useful signals, but something is still missing.

### Low

There is only one weak indicator.

For example:

Same username = Low

Same username + same public name = Better

Same username + same name + same organization = Stronger

Same username + same name + organization + linked public profile = Much stronger

The important part is that the signals should actually be independent.

---

## 24. My Manual Workflow

Target profile

↓

Collect public identifiers

↓

Check followers

↓

Check following

↓

Look for repeated accounts

↓

Check comments

↓

Check mentions

↓

Check tags

↓

Check public highlights

↓

Check public posts

↓

Identify useful connections

↓

Investigate connected accounts

↓

Extract new identifiers

↓

Search new identifiers

↓

Correlate

↓

Verify

↓

Document

---

## 25. What I Don't Do

I don't:

* Assume every follower is a friend
* Assume every interaction proves a relationship
* Guess private family relationships
* Treat one photograph as location proof
* Treat one username match as identity proof
* Treat one reverse-image result as confirmation
* Turn assumptions into facts
* Collect unnecessary private information

The investigation should stay focused on relevant information that is publicly available.

---

## My Point of View

This is where I think manual OSINT becomes much more interesting.

A tool might give me:

Target → Account A

That's only the first lead.

Manual investigation can turn that into:

Target → Account A → Organization → Event → Website → Project → Another public account

The tool helped me find the first connection.

The rest came from following useful public pivots and checking whether each connection actually made sense.

That's why I don't blindly trust automated OSINT results.

Tools are good at finding possibilities.

The analyst's job is deciding which possibilities are useful, which are false positives, and what needs to be verified.

---

## Final Rule

Don't just investigate the target.

Investigate the **public information surrounding the target**.

Followers, following, comments, tags, mentions, highlights, public posts and connected accounts can all become pivots.

But never turn a connection into a fact until the evidence supports it.

**Observe → Pivot → Correlate → Verify → Document**

