
# 01 — Username OSINT

## What is Username OSINT?

Username OSINT is usually one of my first steps when I only have a public username.

For example:

`@redteamerx`

I don't assume that every website using the same username belongs to the same person.

The username is only my starting point.

My basic flow is:

**Username → Search → Possible Matches → Compare → Correlate → Verify**

## 1. Start Manually

Before using any OSINT tool, I search the username myself.

I try the exact username first:

```text
"redteamerx"
````

Then I search where it appears:

```text
"redteamerx" Instagram
"redteamerx" GitHub
"redteamerx" LinkedIn
"redteamerx" Reddit
```

I also search the username without the original platform:

```text
"redteamerx" -instagram.com
```

This can reveal pages that search engines have indexed outside the original platform.

## 2. Look for Username Variations

People don't always use exactly the same username everywhere.

I check variations such as:

```text
redteamerx
redteamerx_
redteamerx123
redteamer_x
redteamer.x
```

I don't treat these as confirmed accounts.

They are only possible pivots.

## 3. What I Compare

When I find a possible account, I compare more than just the username.

I look at:

* Username
* Display name
* Profile picture
* Bio
* Website
* Public location
* Organization
* Interests
* Public posts
* Public projects
* Links to other accounts

If only the username matches, I mark the result as **unconfirmed**.

If several independent details match, my confidence increases.

## 4. The Important Rule

A username is **not an identity**.

For example:

```text
redteamerx → GitHub
```

doesn't automatically mean:

```text
GitHub account = same person
```

It only means:

```text
Possible match → investigate further
```

This is where beginners usually make mistakes.

They find a username on multiple websites and immediately connect everything to one person.

I don't do that.

I collect the lead first, then verify it.

## 5. My Basic Verification Logic

```text
Same username
      ↓
Possible match
      ↓
Same name?
      ↓
Same profile image?
      ↓
Same bio or interests?
      ↓
Same website?
      ↓
Same organization?
      ↓
Independent evidence?
      ↓
Confidence decision
```

The more independent pieces connect, the stronger the correlation becomes.

## 6. My Main Principle

I don't use OSINT tools to give me an answer.

I use them to give me **new pivots**.

One result can lead to another username.

Another username can lead to a public profile.

That profile can reveal a website.

The website can reveal an organization.

The organization can reveal more public information.

That is where username OSINT becomes useful.

---

**My rule:**

> Don't trust the match. Verify the connection.


