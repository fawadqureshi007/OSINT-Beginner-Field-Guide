# 09 — WHOIS & RDAP OSINT

## My Approach

When I find a domain, I want to understand its public registration history and the organizations connected to its registration infrastructure.

I don't treat WHOIS or RDAP as a magic tool that tells me exactly who owns a domain.

Privacy protection, redaction, proxies, corporate registrations and registry policies can hide or replace registrant information.

So I use registration data as **one part of the investigation**.

My basic flow is:

**Domain → RDAP/WHOIS → Registration Data → Correlation → Verification**

---

## 1. What Is WHOIS?

WHOIS is a traditional system for querying domain registration information.

Depending on the domain and registry, it may show information such as:

* Domain
* Registrar
* Registration date
* Updated date
* Expiration date
* Nameservers
* Domain status
* Registrant information
* Administrative information
* Technical information

Modern privacy rules mean much of the personal information may be hidden or redacted.

---

## 2. What Is RDAP?

RDAP stands for:

**Registration Data Access Protocol**

It is the newer standardized system for accessing registration data.

I generally prefer RDAP when available because the response is structured and easier to process.

Instead of relying only on a website, I can query the domain from the terminal.

---

# 3. Install the Basic Tools

On Kali:

```bash
sudo apt update
sudo apt install whois curl jq
```

Check:

```bash
whois --version
curl --version
jq --version
```

---

# 4. Basic WHOIS Query

For a domain:

```bash
whois example.com
```

I don't copy everything blindly.

I look for useful fields such as:

```text
Registrar
Creation Date
Updated Date
Expiration Date
Name Server
Domain Status
```

Some registries format these fields differently.

---

# 5. Search WHOIS Output

Instead of reading a huge response manually:

```bash
whois example.com | less
```

I can search inside `less` with:

```text
/Registrar
```

or:

```text
/Creation
```

or:

```text
/Name Server
```

This is much faster for large responses.

---

# 6. Filter WHOIS Information

I can also use `grep`:

```bash
whois example.com | grep -i "registrar"
```

For nameservers:

```bash
whois example.com | grep -i "name server"
```

For dates:

```bash
whois example.com | grep -Ei "creation|created|updated|expiration|expiry"
```

Different registries use different field names, so I don't expect one exact format everywhere.

---

# 7. RDAP

For many domains, RDAP can be queried through an appropriate registry or registrar RDAP service.

For example, a registry endpoint may look like:

```text
https://rdap.org/domain/example.com
```

Using `curl`:

```bash
curl -s "https://rdap.org/domain/example.com"
```

If the response is JSON, `jq` makes it easier to read:

```bash
curl -s "https://rdap.org/domain/example.com" | jq
```

The exact RDAP server can depend on the TLD.

---

# 8. Why I Prefer Structured RDAP Data

WHOIS output can look different from one domain to another.

RDAP normally provides structured JSON.

That makes it easier to identify:

* Domain
* Status
* Events
* Nameservers
* Entities
* Registrar information

For example:

```bash
curl -s "https://rdap.org/domain/example.com" | jq '.ldhName'
```

The exact fields available can vary.

I inspect the returned JSON rather than assuming every domain has the same data.

---

# 9. Registration Date

One of the first things I check is when the domain was registered.

For example:

```text
Creation Date:
2022-05-10
```

This can help establish a timeline.

If a target's public project appeared in 2023 and the domain was registered in 2022, the dates may be relevant.

But the registration date does **not** prove that the target personally registered the domain.

---

# 10. Updated Date

I also check the update date.

A domain may have been registered years ago but updated recently.

That can indicate changes in registration data, nameservers, status or other domain information.

I treat it as a timeline clue, not proof of who made the change.

---

# 11. Expiration Date

The expiration date can tell me about the current registration period.

Example:

```text
Creation:
2022

Updated:
2025

Expiration:
2027
```

This helps me understand the domain timeline.

Again, it doesn't identify the person operating the website.

---

# 12. Registrar

The registrar is the company through which the domain registration is managed.

Example:

```text
Registrar:
Example Registrar
```

I can then investigate the registrar separately.

Important:

**Registrar ≠ Domain Owner**

The registrar provides registration services.

It doesn't mean the registrar owns the domain.

---

# 13. Nameservers

WHOIS/RDAP can expose nameservers.

Example:

```text
ns1.example-dns.com
ns2.example-dns.com
```

I compare these with the DNS information from the previous chapter.

This gives me another consistency check.

---

# 14. Domain Status

I also check status values.

Common examples include:

```text
clientTransferProhibited
serverTransferProhibited
clientUpdateProhibited
```

These are registration-management statuses.

I don't interpret them as security vulnerabilities.

They mainly tell me about the administrative state of the domain.

---

# 15. Privacy Protection

A common result is:

```text
Registrant:
REDACTED FOR PRIVACY
```

or a privacy/proxy service.

This is normal.

I don't try to bypass it.

Instead, I move to other public sources:

```text
Domain
↓
Website
↓
Public organization
↓
Public social profiles
↓
Public projects
↓
Historical pages
```

The absence of registrant information doesn't end the investigation.

---

# 16. Redacted Registration Data

Modern registration systems may intentionally remove personal information.

I may see:

```text
Name: REDACTED
Email: REDACTED
Phone: REDACTED
```

I record this as:

**Registration information unavailable/redacted.**

I don't attempt to reconstruct private data from unauthorized sources.

---

# 17. Public Organization Registrations

Sometimes the registrant is an organization rather than an individual.

For example:

```text
Registrant Organization:
Example Company Ltd
```

This can become a useful pivot.

I search:

```text
"Example Company Ltd"
```

Then compare:

* Official website
* Public company information
* Public social accounts
* Public projects
* Public documents

---

# 18. Email Addresses

If a WHOIS/RDAP response contains a publicly available email address, I treat it as another identifier.

For example:

```text
admin@example.com
```

I can search the exact public address:

```bash
whois example.com | grep -i "@"
```

Then search it through normal search engines.

I only use addresses that are already publicly exposed.

I don't attempt to discover private email addresses.

---

# 19. Correlating a Public Email

Suppose I find:

```text
admin@example.com
```

Then another public source contains the same address:

```text
example.com
↓
admin@example.com
↓
Public GitHub repository
```

This becomes a useful correlation.

But I still check whether the email is:

* Personal
* Organizational
* Generic
* Automated
* Support-related

A generic address like `support@` doesn't identify a person.

---

# 20. Domain Timeline

I like to build a timeline.

Example:

```text
2022
↓
Domain registered

2023
↓
Public website appears

2024
↓
New project published

2025
↓
Website updated
```

Then I compare this timeline with other public information.

The goal is to see whether the dates are consistent.

---

# 21. WHOIS + DNS

WHOIS tells me about registration.

DNS tells me about the public technical configuration.

I combine them:

```text
Domain
│
├── WHOIS/RDAP
│   ├── Registrar
│   ├── Dates
│   └── Status
│
└── DNS
    ├── A
    ├── MX
    ├── NS
    └── TXT
```

Neither source alone gives me the complete picture.

---

# 22. WHOIS + Certificate Transparency

I can also combine registration data with certificate information.

Example:

```text
Domain
↓
RDAP
↓
Creation date

Domain
↓
Certificate Transparency
↓
Historical hostnames
```

This can help build a better historical timeline.

---

# 23. WHOIS + Search Engines

I also search the domain:

```text
"example.com"
```

Then:

```text
"example.com" cybersecurity
```

And:

```text
"example.com" GitHub
```

Now I have three sources:

```text
RDAP
DNS
Search engine
```

I compare them.

---

# 24. Historical WHOIS

Current WHOIS/RDAP only tells me what is currently available.

Older registration information may have been different.

Historical WHOIS services can sometimes provide previous records, depending on availability and coverage.

I use historical data carefully because:

* Records may be incomplete
* Ownership may have changed
* Privacy services may have been used
* Data may have been corrected
* Different services may have different histories

Historical information needs date-aware verification.

---

# 25. Ownership Changes

A domain can change hands.

For example:

```text
2019
Person/Organization A

2022
Privacy-protected registration

2025
Organization B
```

I don't automatically connect all historical records to one person.

The correct question is:

**Who was associated with the domain during this specific period?**

---

# 26. Domain Transfers

A domain can move between registrars without changing ownership.

For example:

```text
Registrar A
↓
Registrar B
```

This doesn't automatically mean:

```text
Owner A
↓
Owner B
```

Registrar changes and ownership changes are different things.

---

# 27. Nameserver Changes

Historical DNS or domain information may show nameserver changes.

For example:

```text
2022
ns1.provider-a.com

2024
ns1.provider-b.com
```

This can indicate infrastructure changes.

It does not necessarily mean ownership changed.

---

# 28. Domain Status Changes

Status history can sometimes provide additional timeline information.

I record:

* Current status
* Historical status when available
* Relevant dates

But I don't interpret normal registration statuses as evidence of malicious activity.

---

# 29. RDAP JSON With jq

For people who want to understand the raw data:

```bash
curl -s "https://rdap.org/domain/example.com" | jq '.'
```

To inspect the domain name:

```bash
curl -s "https://rdap.org/domain/example.com" | jq '.ldhName'
```

To inspect nameservers:

```bash
curl -s "https://rdap.org/domain/example.com" | jq '.nameservers'
```

To inspect events:

```bash
curl -s "https://rdap.org/domain/example.com" | jq '.events'
```

The exact response structure can differ, so I inspect the actual JSON before writing a parser.

---

# 30. Save the Result

For documentation:

```bash
curl -s "https://rdap.org/domain/example.com" > rdap-example.json
```

WHOIS:

```bash
whois example.com > whois-example.txt
```

DNS:

```bash
dig example.com > dns-example.txt
```

Now I have local evidence of what I observed at that point in time.

I record the date of collection because registration and DNS information can change.

---

# 31. Create a Simple Domain Record

For every investigation I can maintain:

```text
Domain:
example.com

Registrar:
Example Registrar

Created:
YYYY-MM-DD

Updated:
YYYY-MM-DD

Expires:
YYYY-MM-DD

Nameservers:
ns1.example.com
ns2.example.com

Status:
Current status

Registrant:
Public / Redacted

Source:
RDAP / WHOIS

Collected:
YYYY-MM-DD
```

This makes the investigation much easier to review later.

---

# 32. Confidence

I use the same evidence model throughout my OSINT work.

### Low

Only one weak registration clue.

### Medium

Registration data matches another public identifier.

### High

Registration information, public organization information and independent public sources all agree.

I don't increase confidence just because I found more copies of the same information.

---

# 33. What WHOIS Cannot Tell Me

WHOIS/RDAP usually cannot prove:

* Who physically operates a website
* Who wrote a particular article
* Who controls an anonymous account
* Who is behind an IP address
* Who actually uses a mailbox
* Who owns the hosting account

Registration information is only one part of the picture.

---

# 34. Common Mistakes

### Mistake 1

Assuming the registrar owns the domain.

Wrong.

### Mistake 2

Assuming the registrant name is automatically the person operating the site.

Not necessarily.

### Mistake 3

Assuming a hidden registrant means the domain has no useful information.

Wrong.

There are many other public pivots.

### Mistake 4

Treating an old WHOIS record as current.

Always check dates.

### Mistake 5

Ignoring domain ownership changes.

Historical attribution matters.

---

# 35. My Practical Workflow

```text
Domain
↓
WHOIS
↓
RDAP
↓
Registrar
↓
Creation / Update / Expiration
↓
Nameservers
↓
Status
↓
Public registrant information
↓
Historical records
↓
DNS correlation
↓
Certificate correlation
↓
Search-engine correlation
↓
Organization / project correlation
↓
Verification
↓
Documentation
```

---

# My Point of View

WHOIS and RDAP are not about finding a magic name behind a domain.

Sometimes the registrant information is completely hidden.

Sometimes it is an organization.

Sometimes it is a privacy service.

Sometimes the information is useful.

Sometimes it gives me almost nothing.

I don't force the investigation when the data isn't there.

Instead, I use whatever legitimate public information is available and pivot somewhere else.

For me, the value is in combining small pieces:

**Domain → Registration date → Nameservers → DNS → Certificates → Public website → Organization → Other public sources**

One record rarely tells the whole story.

The correlation does.

---

# Final Rule

**Never treat WHOIS/RDAP as identity proof.**

Use it to establish registration facts and build a timeline.

Then correlate those facts with independent public sources.

**Query → Extract → Correlate → Verify → Document**
