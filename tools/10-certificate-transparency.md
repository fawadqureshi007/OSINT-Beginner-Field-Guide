# 10 — Certificate Transparency OSINT

## My Approach

When I find a domain, I don't only check DNS.

I also check **Certificate Transparency (CT) logs**.

A website using HTTPS normally has a TLS certificate. Public Certificate Transparency systems record certificates so that certificate issuance can be monitored and audited.

For OSINT, this can be useful because a certificate may contain hostnames that I didn't find through normal searches.

For example:

```text
example.com
↓
Certificate
↓
www.example.com
api.example.com
dev.example.com
mail.example.com
```

That gives me new public pivots.

The important part:

**A certificate is a clue, not proof of ownership by a particular person.**

---

# 1. What Certificate Transparency Gives Me

Depending on the certificate, I may find:

* Main domain
* `www` hostname
* Subdomains
* Wildcard names
* Alternative names
* Older hostnames
* Certificate dates
* Issuer
* Certificate status/history

The most interesting part for OSINT is usually the **hostname information**.

---

# 2. Start With crt.sh

One of the easiest places to begin is:

```text
crt.sh
```

Search for:

```text
example.com
```

I look through the certificates and check the names included in them.

I don't assume every result is currently active.

Some certificates can be expired or historical.

---

# 3. Search From the Browser

I can search:

```text
%.example.com
```

or:

```text
example.com
```

depending on the CT search interface.

The goal is to find certificate entries associated with the domain.

I record:

* Certificate ID
* Common Name
* Subject Alternative Names
* Issuer
* Not Before
* Not After

---

# 4. Search CT Data From the Command Line

For `crt.sh`, I can query the public JSON endpoint:

```bash
curl -s "https://crt.sh/?q=%25.example.com&output=json"
```

The `%25` represents `%` in the URL encoding.

I can make the output easier to inspect with:

```bash
curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq
```

---

# 5. Extract Certificate Names

A certificate can contain multiple names.

For example, I can inspect the `name_value` field:

```bash
curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq -r '.[].name_value'
```

This may return something like:

```text
example.com
www.example.com
api.example.com
dev.example.com
```

The exact results depend on the domain.

---

# 6. Remove Duplicates

The same hostname can appear in multiple certificates.

I normally remove duplicates:

```bash
curl -s "https://crt.sh/?q=%25.example.com&output=json" \
| jq -r '.[].name_value' \
| sort -u
```

Now I have a cleaner hostname list.

---

# 7. Save the Results

I can save the output:

```bash
curl -s "https://crt.sh/?q=%25.example.com&output=json" \
| jq -r '.[].name_value' \
| sort -u > ct-hostnames.txt
```

Then:

```bash
cat ct-hostnames.txt
```

This gives me a simple list to correlate with other sources.

---

# 8. Wildcard Certificates

I may see:

```text
*.example.com
```

This means the certificate covers subdomains under that domain.

It does **not** mean that every possible subdomain exists.

For example:

```text
*.example.com
```

doesn't prove that:

```text
secret.example.com
```

exists.

I still need to verify actual hostnames through public DNS or other evidence.

---

# 9. Subject Alternative Names

Modern certificates can contain multiple names.

For example:

```text
example.com
www.example.com
api.example.com
portal.example.com
```

These are often more useful than looking only at the certificate's main name.

I always inspect the complete set of names when available.

---

# 10. Historical Hostnames

This is where CT becomes particularly interesting.

Suppose I find:

```text
old-api.example.com
```

but DNS no longer resolves it.

That doesn't necessarily mean the result is useless.

It may indicate that the hostname existed publicly at some point.

I record it as:

**Historical certificate evidence**

rather than:

**Currently active host**

---

# 11. Certificate Dates

I check:

```text
Not Before
Not After
```

These dates help establish when a certificate was valid.

For example:

```text
Not Before:
2023-04-01

Not After:
2024-04-01
```

This can help build an infrastructure timeline.

---

# 12. Build a Timeline

I can combine certificate history:

```text
2022
↓
example.com certificate

2023
↓
api.example.com appears

2024
↓
dev.example.com certificate

2025
↓
new infrastructure appears
```

Then I compare this with:

* Domain registration
* DNS changes
* Website history
* Public projects
* Organization activity

The dates don't prove causation.

They help establish chronology.

---

# 13. Find New Pivots

Suppose the original domain is:

```text
example.com
```

CT reveals:

```text
api.example.com
dev.example.com
portal.example.com
```

Now each hostname becomes a new public pivot.

I can check:

```bash
dig A api.example.com
```

```bash
dig A dev.example.com
```

```bash
dig A portal.example.com
```

I am not assuming that all of them are currently active.

I'm verifying what is publicly observable.

---

# 14. CT + DNS

This is one of my favorite combinations.

```text
Certificate Transparency
        ↓
api.example.com
        ↓
DNS lookup
        ↓
Current DNS result
```

If CT says a hostname existed and DNS currently resolves it, confidence that the hostname is currently active increases.

If CT shows it but DNS doesn't resolve it, I mark it as historical or unconfirmed.

---

# 15. CT + WHOIS/RDAP

I can combine:

```text
RDAP
↓
Domain registration date
```

with:

```text
CT
↓
First certificate evidence
```

Example:

```text
Domain registered:
2022

Certificate observed:
2023
```

This gives me a basic infrastructure timeline.

Again, it doesn't identify the individual operating the domain.

---

# 16. CT + Search Engines

If CT gives me:

```text
portal.example.com
```

I search it:

```text
"portal.example.com"
```

Then:

```text
site:example.com "portal"
```

I may find public pages, documentation, articles or references.

The search engine becomes another independent source.

---

# 17. CT + GitHub

If I discover:

```text
api.example.com
```

I can search:

```text
"api.example.com" site:github.com
```

I may find public:

* Documentation
* README files
* Example projects
* Public configuration references

I don't use exposed credentials or secrets.

The purpose here is public correlation.

---

# 18. Search Certificate Names Directly

Sometimes the hostname itself is the best search term:

```text
"dev.example.com"
```

or:

```text
"api.example.com"
```

Then:

```text
"api.example.com" GitHub
```

and:

```text
"api.example.com" documentation
```

A hostname can appear in public technical documentation long after it was originally created.

---

# 19. Check Certificate Issuers

Certificates also contain issuer information.

For example:

```text
Issuer:
Let's Encrypt
```

or another certificate authority.

I record the issuer because it helps describe the certificate infrastructure.

But:

**Certificate Authority ≠ Website Owner**

The CA issued the certificate.

It does not mean the CA operates the website.

---

# 20. Check Multiple Certificates

One hostname can have several certificates over time.

For example:

```text
api.example.com
↓
Certificate 1
↓
Certificate 2
↓
Certificate 3
```

This can happen because certificates expire and are renewed.

I don't count every certificate as a separate asset.

I normalize the hostnames first.

---

# 21. Extract Unique Hostnames

A simple workflow:

```bash
curl -s "https://crt.sh/?q=%25.example.com&output=json" \
| jq -r '.[].name_value' \
| tr '\r' '\n' \
| sort -u
```

Depending on the returned data, wildcard entries may also appear.

I can inspect them separately rather than blindly treating them as active hosts.

---

# 22. Save Raw Evidence

I prefer saving the original response as well:

```bash
curl -s "https://crt.sh/?q=%25.example.com&output=json" > certificates.json
```

Then:

```bash
jq '.[0]' certificates.json
```

Now I have the original structured result available for documentation.

I also record the collection date.

---

# 23. Basic Python Parsing

If I want to process a saved CT response:

```python
import json

with open("certificates.json", "r") as f:
    data = json.load(f)

names = set()

for cert in data:
    for name in cert.get("name_value", "").splitlines():
        names.add(name.strip())

for name in sorted(names):
    print(name)
```

This is useful when I want to build a larger OSINT workflow later.

---

# 24. Other CT Sources

`crt.sh` is easy for beginners, but it isn't the only source.

Other places to research CT data include:

* Censys
* Google CT ecosystem
* Certificate Transparency monitors
* Public certificate databases

I don't depend on one source if the investigation is important.

Different services can have different interfaces, search capabilities and historical coverage.

---

# 25. Censys

Censys provides public internet and certificate-related search capabilities.

I can search for a domain or certificate-related identifier and compare what I find with CT results.

For example, if CT gives me:

```text
api.example.com
```

I can investigate that hostname through another public source.

The goal is correlation.

Not collecting the same result from ten different websites.

---

# 26. Certificate Transparency Does Not Equal DNS

This distinction is extremely important.

CT:

```text
Certificate was publicly logged
```

DNS:

```text
Hostname currently has a DNS record
```

These are different facts.

A hostname can exist in CT but no longer exist in DNS.

Therefore:

**CT result ≠ active host**

---

# 27. Certificate Transparency Does Not Equal Ownership

Another important rule:

```text
Certificate
≠
Person
```

Finding:

```text
api.example.com
```

doesn't prove that a particular individual controls it.

I need other independent public evidence before making that connection.

---

# 28. False Positives

CT results can contain:

* Wildcards
* Old hostnames
* Shared infrastructure
* Third-party services
* Mistyped names
* Historical infrastructure
* Hostnames that are no longer active

So I never copy the complete CT result into my final intelligence report without verification.

---

# 29. My Confidence Model

### Low

Hostname appears only in a CT record.

### Medium

Hostname appears in CT and another public source.

### High

Hostname appears in CT, resolves publicly, and is independently associated with the same organization/domain through reliable public sources.

This keeps the investigation evidence-based.

---

# 30. What I Look For

When reviewing CT results, I pay attention to names such as:

```text
api.example.com
dev.example.com
staging.example.com
portal.example.com
docs.example.com
mail.example.com
blog.example.com
```

These names can reveal how an organization publicly structures its online services.

But I don't assume that a hostname such as `dev` means an actual development server is currently exposed.

The name itself is only a clue.

---

# 31. My Practical Workflow

```text
Target
↓
Find Domain
↓
Search Certificate Transparency
↓
Collect Certificate Names
↓
Normalize Hostnames
↓
Remove Duplicates
↓
Separate Wildcards
↓
Check Certificate Dates
↓
Check DNS
↓
Search Hostnames
↓
Correlate With WHOIS/RDAP
↓
Correlate With Public Websites
↓
Verify
↓
Document
```

---

# 32. My Investigation Notes

For every interesting hostname I record:

```text
Hostname:
api.example.com

Source:
Certificate Transparency

Certificate:
ID / reference

Issuer:
Certificate Authority

First observed:
Date

Last observed:
Date

Current DNS:
Yes / No

Other public references:
URL / source

Confidence:
Low / Medium / High
```

This prevents me from mixing historical information with current infrastructure.

---

# 33. What I Don't Do

I don't:

* Treat CT results as proof of ownership
* Assume every hostname is currently active
* Attack discovered services
* Brute-force certificate-related hosts
* Bypass authentication
* Use CT data to access private systems
* Treat wildcard certificates as actual hostnames
* Publish unnecessary personal information

Certificate Transparency is an **information source**, not an authorization bypass.

---

# My Point of View

Certificate Transparency is one of those OSINT sources that looks boring until you connect it with everything else.

I may start with:

```text
example.com
```

CT can give me:

```text
api.example.com
dev.example.com
portal.example.com
old.example.com
```

Then I check:

```text
CT
↓
DNS
↓
Search engines
↓
Public repositories
↓
Website
↓
WHOIS/RDAP
↓
Historical sources
```

Now the certificate isn't just a certificate anymore.

It's another piece of the infrastructure timeline.

But I never forget the most important rule:

**A certificate tells me something about public certificate issuance. It does not automatically tell me who is behind the system.**

Good OSINT comes from connecting that clue with independent evidence.

---

# Final Rule

**Don't treat CT as a list of live targets. Treat it as a historical public record of certificate issuance.**

Use it to discover hostnames.

Verify them with DNS and other public sources.

Separate current infrastructure from historical infrastructure.

Then document exactly where every finding came from.

**Domain → CT → Hostnames → DNS → Historical Context → Correlation → Verification → Documentation**
