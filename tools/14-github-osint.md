# 14 — GitHub OSINT

## My Approach

GitHub is not only a place for code.

For OSINT, a public GitHub profile can connect usernames, projects, organizations, websites, domains, technologies, public activity and development history.

I don't start by looking at everything.

I start with one identifier and follow the useful pivots.

My basic flow:

**Username → GitHub → Profile → Repositories → Commits → Projects → Contributors → Organizations → Domains → Correlation → Verification**

---

# 1. Start With a Username

If I already have:

```text
redteamerx
```

I search for it directly:

```text
"redteamerx" GitHub
```

I can also search:

```text
"redteamerx" site:github.com
```

The goal at this stage is **discovery**, not attribution.

Finding the username on GitHub doesn't automatically prove it belongs to the same person.

---

# 2. Verify the GitHub Profile

Once I find a possible profile, I compare public information.

I check:

```text
Username
Display name
Profile picture
Bio
Location
Website
Organization
Public repositories
Activity
```

If several identifiers match the original target, confidence increases.

For example:

```text
Same username
+
Same public name
+
Same website
+
Same project
```

is much stronger than:

```text
Same username
```

---

# 3. GitHub Search

GitHub itself is useful for discovering public repositories and users.

I search for:

```text
redteamerx
```

Then project names:

```text
"BlackTrace"
```

And combinations:

```text
"BlackTrace" "Fawad Qureshi"
```

I also search exact phrases from public bios or project descriptions.

---

# 4. Search Engines + GitHub

I don't rely only on GitHub's own search.

I also use search engines:

```text
"redteamerx" site:github.com
```

```text
"Fawad Qureshi" site:github.com
```

```text
"BlackTrace" site:github.com
```

This can sometimes surface:

* Profiles
* Repositories
* Issues
* Pull requests
* Documentation
* Cached references
* Other public GitHub pages

---

# 5. Profile Information

A public GitHub profile can provide useful identifiers.

I record only what is relevant:

```text
Username:
Display name:
Bio:
Website:
Organization:
Public location:
Repositories:
```

Then I look for connections.

Example:

```text
GitHub username
↓
Website
↓
Domain
```

That domain becomes a new OSINT pivot.

---

# 6. Public Repositories

Repositories are often the biggest source of information.

I check:

```text
Repository name
Description
Owner
Creation date
Last update
Languages
README
Contributors
Releases
Issues
Pull requests
Website
```

A project name can lead to another public source.

---

# 7. Repository → Project Pivot

Suppose I find:

```text
BlackTrace
```

I search:

```text
"BlackTrace"
```

Then:

```text
"BlackTrace" cybersecurity
```

Then:

```text
"BlackTrace" "Fawad Qureshi"
```

This can connect a repository with:

* Social profiles
* Websites
* Articles
* Conferences
* Documentation
* Other projects

---

# 8. README Files

I always read the README.

It may contain:

```text
Project author
Website
Documentation
Social links
Organization
Contact information
Technology
Installation instructions
Related projects
```

The README can create several new pivots.

I don't assume every name mentioned in a README is the repository owner.

---

# 9. Repository Links

I look for links such as:

```text
Website
Documentation
Demo
GitHub Pages
Social profile
Project organization
```

For example:

```text
GitHub Repository
↓
Website
↓
Domain
↓
DNS
```

Now I can move into the domain/DNS chapters.

---

# 10. Contributors

A repository may have multiple public contributors.

I check:

```text
Owner
Contributors
Pull requests
Commit authors
```

But I don't assume:

```text
Contributor = Owner
```

A person may contribute to a project without owning it.

---

# 11. Commit History

The commit history can provide useful public development information.

From a **public repository**:

```bash
git clone https://github.com/USER/REPOSITORY.git
```

Then:

```bash
cd REPOSITORY
```

View commits:

```bash
git log
```

Compact view:

```bash
git log --oneline
```

This helps me understand the public development timeline.

---

# 12. `git shortlog`

I can summarize commit authors:

```bash
git shortlog -sne
```

This can show public commit author names/emails associated with the repository's Git history.

I treat these as leads.

A commit email does not automatically prove ownership of a GitHub account.

---

# 13. Inspect a Commit

For a specific commit:

```bash
git show COMMIT_ID
```

I can inspect:

* Commit message
* Author
* Date
* Changes
* Files modified

I use this for understanding public project history.

---

# 14. Commit Timeline

Commit timestamps can help establish:

```text
Project started
↓
Major development
↓
Release
↓
Public announcement
```

I compare this timeline with other public sources.

For example:

```text
GitHub commit:
June 2025

Public announcement:
July 2025
```

This gives useful chronology.

---

# 15. Public Commit Email

Git history may contain an email address.

For example:

```text
Author: Example Name <example@example.com>
```

If the address is already publicly exposed through the repository history, it can become a correlation pivot.

I can search:

```text
"example@example.com"
```

Then compare the results with other public sources.

I don't use an exposed email to access accounts.

---

# 16. Git Configuration

For a local copy of a public repository, I can inspect Git configuration:

```bash
git config --list
```

Repository-specific configuration:

```bash
git config --local --list
```

I don't treat local configuration as evidence about the public repository owner.

It may reflect the machine on which I cloned or modified the repository.

---

# 17. Remote Repository

Check the configured remote:

```bash
git remote -v
```

This can confirm which public repository the local copy is connected to.

---

# 18. Search the Repository

After cloning a public repository, I can search its files:

```bash
git grep -n "keyword"
```

For example:

```bash
git grep -n "github.com"
```

or:

```bash
git grep -n "example.com"
```

This can find publicly documented links and references.

---

# 19. Search Project Names

A project name is often a better pivot than a person's name.

For example:

```text
"BlackTrace"
```

Then search:

```text
"BlackTrace" GitHub
```

```text
"BlackTrace" website
```

```text
"BlackTrace" developer
```

```text
"BlackTrace" cybersecurity
```

I compare the results rather than assuming every result refers to the same project.

---

# 20. Organizations

GitHub organizations can reveal another layer of public information.

I check:

```text
Organization name
Public repositories
Members where publicly visible
Projects
Websites
Related domains
```

Then:

```text
Person
↓
GitHub
↓
Organization
↓
Public repositories
↓
Website
```

---

# 21. GitHub Pages

Some public repositories use GitHub Pages.

A repository may connect to:

```text
username.github.io
```

or another public custom domain.

That can become a domain pivot:

```text
GitHub
↓
GitHub Pages
↓
Website
↓
Domain
```

---

# 22. Releases

I check public releases because they can show:

* Version numbers
* Release dates
* Project history
* Release notes
* Contributors
* Documentation links

Example:

```text
v1.0
↓
2024
↓
v2.0
↓
2025
```

This helps establish project chronology.

---

# 23. Issues

Public issues can contain useful project context.

I look for:

```text
Bug reports
Feature requests
Maintainers
Contributors
Project references
Related repositories
```

I don't treat every person commenting on an issue as part of the organization.

They may simply be a community member.

---

# 24. Pull Requests

Public pull requests can show:

```text
Contributor
Date
Project
Code contribution
Discussion
Reviewers
```

Again:

**Contribution ≠ ownership.**

I use pull requests to establish public involvement with a project, not automatically someone's identity.

---

# 25. Forks

Forks can reveal relationships between public repositories.

For example:

```text
Original Project
↓
Fork
↓
Another Username
```

This can create a new investigation pivot.

But a fork only shows that a public repository was copied/forked.

It doesn't automatically establish a personal relationship between the users.

---

# 26. Stars

Stars can sometimes help understand a public account's interests.

I treat them as contextual information rather than strong identity evidence.

For serious attribution, I prefer stronger connections such as:

```text
Username
+
Project
+
Website
+
Public identity
```

---

# 27. Repository Dates

I record:

```text
Created
Updated
Released
Committed
```

Then compare with other public sources.

Example:

```text
GitHub project created:
2025

Instagram announcement:
2025

Website launched:
2025
```

A consistent timeline can increase confidence.

---

# 28. Languages and Technologies

GitHub shows languages used in public repositories.

For example:

```text
Python
JavaScript
C++
Shell
Java
```

I can use this to understand the public technical footprint.

I don't use a programming language alone to identify someone.

---

# 29. Public Configuration Information

Some repositories contain configuration files intended for public use.

I may inspect:

```text
README
requirements.txt
package.json
Dockerfile
config examples
documentation
```

These can reveal:

* Technology
* Dependencies
* Project architecture
* Public domains
* APIs referenced in documentation

I avoid turning this into unauthorized access.

---

# 30. Secrets and Credentials

This is an important boundary.

If a public repository appears to contain:

```text
API key
Password
Private token
Cloud credential
SSH private key
```

I **do not use it to access anything**.

For OSINT documentation, I can record that a credential appears to have been publicly exposed and recommend responsible disclosure.

I don't provide instructions for using the credential.

---

# 31. Search Engine GitHub Queries

Useful examples:

```text
"redteamerx" site:github.com
```

```text
"Fawad Qureshi" site:github.com
```

```text
"BlackTrace" site:github.com
```

```text
"example@example.com" site:github.com
```

```text
"example.com" site:github.com
```

The idea is to combine identifiers.

---

# 32. GitHub API

GitHub provides APIs for publicly available information.

For example, public user information can be queried through GitHub's API.

A basic request:

```bash
curl https://api.github.com/users/USERNAME
```

For a public repository:

```bash
curl https://api.github.com/repos/OWNER/REPOSITORY
```

The API is useful when I need structured information instead of manually reading pages.

---

# 33. API + JSON Tools

If I want to inspect the response:

```bash
curl -s https://api.github.com/users/USERNAME
```

If `jq` is installed:

```bash
curl -s https://api.github.com/users/USERNAME | jq
```

I can extract individual fields from public API responses.

---

# 34. GitHub Rate Limits

Automated requests can be rate limited.

If I'm doing serious research, I don't hammer the service.

I use:

* Reasonable request rates
* Public APIs properly
* Authentication where appropriate for legitimate API usage
* Caching when possible

OSINT doesn't mean sending thousands of unnecessary requests.

---

# 35. GitLab

The same general methodology works with GitLab.

I can investigate:

```text
Username
Profile
Projects
Repositories
Commits
Contributors
Issues
Merge requests
Organizations/groups
Public websites
```

The interface is different, but the OSINT principles remain the same.

---

# 36. GitHub → Domain Pivot

Suppose a repository contains:

```text
example.com
```

Now I move:

```text
GitHub
↓
Repository
↓
Website
↓
Domain
↓
DNS
↓
Certificate Transparency
```

The domain becomes the next investigation category.

---

# 37. GitHub → Social Pivot

A public README may contain:

```text
Instagram
X
LinkedIn
Telegram
Website
```

I compare those public profiles with the original target.

Again, one matching username is not enough.

---

# 38. GitHub → Organization Pivot

A repository may belong to an organization:

```text
User
↓
Repository
↓
Organization
↓
Other public repositories
↓
Projects
↓
Website
```

This can expose a much broader public footprint.

---

# 39. GitHub → Project → Person

The reverse can also happen.

I may start with:

```text
Project name
```

Then:

```text
Project
↓
GitHub
↓
Contributors
↓
Public profiles
```

This is useful when I don't know the developer's username yet.

---

# 40. Don't Trust Names Alone

Suppose a repository has:

```text
Fawad Qureshi
```

There may be many people with that name.

I need additional context:

```text
Name
+
Username
+
Project
+
Website
+
Organization
```

The more independent identifiers match, the stronger the attribution.

---

# 41. My GitHub Evidence Table

I record:

| Finding         | Source         | Pivot        | Confidence |
| --------------- | -------------- | ------------ | ---------- |
| GitHub username | Public profile | Username     | Medium     |
| Project         | Repository     | Project      | High       |
| Website         | README         | Domain       | High       |
| Contributor     | Commit history | Developer    | Medium     |
| Organization    | Public profile | Organization | Medium     |

This makes my conclusions easier to audit.

---

# 42. My Verification Rule

For every important GitHub finding:

```text
Discovery
↓
Check GitHub source
↓
Find independent public source
↓
Compare identifiers
↓
Check timeline
↓
Assign confidence
```

I don't let a GitHub result become a fact just because GitHub displayed it.

---

# 43. My Practical Workflow

```text
Username / Name / Project
↓
Search GitHub
↓
Identify possible profile
↓
Verify public identifiers
↓
Inspect repositories
↓
Read README
↓
Check contributors
↓
Check commits
↓
Check public links
↓
Check organizations
↓
Check releases/issues/PRs
↓
Extract new public pivots
↓
Search those pivots elsewhere
↓
Correlate
↓
Verify
↓
Document
```

---

# 44. My Point of View

GitHub is one of the best OSINT sources for technical targets because one public repository can connect many different pieces:

```text
Username
↓
GitHub
↓
Repository
↓
Project
↓
Contributor
↓
Public commit
↓
Website
↓
Domain
↓
Organization
```

But I don't confuse **visibility with attribution**.

A repository is public.

A username is public.

A commit is public.

A project is public.

The actual intelligence comes from proving that these pieces belong to the same entity.

---

# Final Rule

**GitHub is a source of public clues, not automatic identity proof.**

My workflow is:

```text
Find
↓
Inspect
↓
Pivot
↓
Correlate
↓
Verify
↓
Document
```

And my biggest rule:

> **A username match is a lead. A repository match is a lead. A commit match is a lead. Multiple independent public connections are what turn those leads into useful intelligence.**
