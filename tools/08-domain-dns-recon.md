# 08 — Domain & DNS Reconnaissance

## My Approach

When I find a domain connected to a target, I treat the domain as a completely new OSINT pivot.

I don't jump straight into aggressive scanning.

First I collect what is already publicly available:

* Domain
* Subdomains
* DNS records
* Nameservers
* Mail servers
* Certificate names
* Public technologies
* Organization information
* Public repositories
* Historical references

The domain can connect several parts of the investigation:

**Target → Username → Website → Domain → DNS → Subdomains → Certificates → Public infrastructure**

The important rule is:

**Finding a domain does not automatically prove ownership.**

I verify the connection before attributing the infrastructure to the target.

---

## 1. Start With the Domain

If I discover:

```text
example.com
```

I first open the public website and record:

* Domain
* Homepage
* About page
* Contact page
* Organization name
* Public email
* Social links
* Technology clues
* Public projects
* Copyright information

Then I search the domain itself:

```text
"example.com"
```

This can reveal public pages that don't appear directly from the website.

---

## 2. Check DNS

DNS can expose useful public infrastructure information.

On Kali/Linux I can use:

```bash
dig example.com
```

For common record types:

```bash
dig A example.com
dig AAAA example.com
dig MX example.com
dig NS example.com
dig TXT example.com
```

I can also request all commonly available records:

```bash
dig ANY example.com
```

However, many DNS servers don't return complete information for `ANY`, so I don't depend on it.

---

## 3. Understand the Main DNS Records

### A

Points a domain to an IPv4 address.

```bash
dig A example.com
```

### AAAA

Points to an IPv6 address.

```bash
dig AAAA example.com
```

### MX

Shows publicly configured mail servers.

```bash
dig MX example.com
```

### NS

Shows authoritative nameservers.

```bash
dig NS example.com
```

### TXT

May contain publicly configured text records.

```bash
dig TXT example.com
```

TXT records can contain things such as domain verification or email-security information.

I don't assume that every TXT record contains something useful.

---

## 4. Reverse DNS

If I discover a public IP address, I can check whether it has a reverse DNS name:

```bash
dig -x IP_ADDRESS
```

For example:

```bash
dig -x 203.0.113.10
```

A reverse DNS result can provide another hostname to investigate.

It is another pivot, not automatically proof of ownership.

---

## 5. Check Nameservers

I check:

```bash
dig NS example.com
```

Nameservers can tell me which DNS provider or infrastructure is being used.

Then I can investigate the public organization behind that service.

I don't assume that the DNS provider is the owner of the domain.

---

## 6. Check Mail Servers

I check:

```bash
dig MX example.com
```

This can reveal publicly configured mail infrastructure.

For example:

```text
example.com
↓
MX record
↓
mail provider
```

This can help understand how the domain's public email infrastructure is configured.

I don't attempt to access mailboxes.

---

## 7. TXT Records

I check:

```bash
dig TXT example.com
```

TXT records may contain:

* SPF
* Domain verification
* Service verification
* Public configuration information

For example, an SPF record can show which systems are authorized to send email for the domain.

This is useful for understanding the public configuration, not for attacking the mail system.

---

## 8. Subdomain Enumeration

Subdomains can reveal additional public services.

Examples:

```text
www.example.com
mail.example.com
blog.example.com
docs.example.com
dev.example.com
api.example.com
```

I can use passive sources to discover publicly indexed subdomains.

Useful tools include:

* Amass
* Subfinder
* assetfinder

I prefer passive enumeration when doing normal OSINT because it reduces unnecessary interaction with the target infrastructure.

---

## 9. Subfinder

### Installation

On Kali, availability can vary by package version. If installed through the package manager:

```bash
sudo apt update
sudo apt install subfinder
```

If the package isn't available, use the official project installation instructions rather than downloading random binaries.

### Basic usage

```bash
subfinder -d example.com
```

Save results:

```bash
subfinder -d example.com -o subdomains.txt
```

The important option here is:

```text
-d
```

which specifies the domain.

---

## 10. Amass

Amass is another well-known reconnaissance framework.

For passive enumeration:

```bash
amass enum -passive -d example.com
```

Save results:

```bash
amass enum -passive -d example.com -o amass.txt
```

I prefer the passive mode when the objective is public-source reconnaissance.

---

## 11. Compare Multiple Sources

I don't automatically trust one enumeration tool.

For example:

```text
Subfinder
↓
sub1.example.com
sub2.example.com

Amass
↓
sub2.example.com
sub3.example.com
```

The combined list becomes:

```text
sub1.example.com
sub2.example.com
sub3.example.com
```

Repeated results across independent sources can increase confidence that a hostname is publicly associated with the domain.

---

## 12. Check DNS for Discovered Subdomains

If I find:

```text
dev.example.com
```

I can check:

```bash
dig A dev.example.com
```

Then:

```bash
dig CNAME dev.example.com
```

This can show whether the hostname points somewhere else.

Again, I record the information instead of immediately interacting with the service.

---

## 13. CNAME Records

A CNAME can reveal that a hostname points to another public hostname.

Example:

```bash
dig CNAME blog.example.com
```

Possible structure:

```text
blog.example.com
↓
provider.example.net
```

This can reveal hosting or SaaS relationships.

It doesn't automatically reveal the physical server or private infrastructure.

---

## 14. Certificate Transparency

TLS certificates can contain hostnames associated with a domain.

I can use public Certificate Transparency sources to search:

```text
example.com
```

This may reveal names such as:

```text
www.example.com
api.example.com
dev.example.com
staging.example.com
```

Certificate records can therefore become another source for passive subdomain discovery.

I'll cover this in much more detail in the next chapter.

---

## 15. Search the Domain With Search Engines

I also combine DNS discoveries with search engines.

For example:

```text
site:example.com
```

Or:

```text
site:example.com "login"
```

Or:

```text
site:example.com filetype:pdf
```

This can reveal publicly indexed content associated with the domain.

I don't attempt to access restricted areas.

---

## 16. Search the Domain as an Exact Phrase

I can search:

```text
"example.com"
```

Then:

```text
"example.com" GitHub
```

```text
"example.com" "Fawad Qureshi"
```

```text
"example.com" cybersecurity
```

This can reveal public references outside the website itself.

---

## 17. Public GitHub References

If I find a domain, I search for it on public code-hosting platforms.

For example:

```text
"example.com" site:github.com
```

I may discover:

* Public repositories
* README files
* Documentation
* Public configuration examples
* Project pages

I don't use discovered secrets or credentials.

If something sensitive appears publicly, I document the exposure responsibly rather than using it.

---

## 18. Technology Fingerprinting

I can inspect the public website to understand what technologies are visible.

Useful tools include:

* WhatWeb
* Wappalyzer
* Browser developer tools

For example:

```bash
whatweb https://example.com
```

This may identify publicly observable technologies such as:

* Web servers
* Frameworks
* CMS
* JavaScript libraries

Technology identification can help explain the public technical footprint.

It isn't a vulnerability assessment by itself.

---

## 19. Check HTTP Headers

For a website I am authorized to inspect, I can view public HTTP headers:

```bash
curl -I https://example.com
```

I look for information such as:

* Server
* Redirects
* Content type
* Security headers
* Caching information

Headers are useful for fingerprinting the public web stack.

---

## 20. Don't Confuse Hosting With Ownership

This is important.

Suppose:

```text
example.com
↓
Cloud provider
↓
Shared infrastructure
```

That does not mean the cloud provider owns the organization.

Similarly, an IP address does not automatically identify the person behind a website.

I distinguish between:

**Domain owner**

**Hosting provider**

**DNS provider**

**Certificate authority**

**Infrastructure provider**

These are different things.

---

## 21. Organization Pivot

If the website identifies an organization:

```text
Domain
↓
Organization
```

I search the organization separately.

I can check its public:

* Website
* Social profiles
* GitHub
* LinkedIn
* Projects
* Public documents
* Events

The domain becomes the bridge between the original target and the organization.

---

## 22. Historical Domain Information

If I need historical context, I look for publicly available historical sources.

Useful sources can include:

* Web archives
* Historical DNS databases
* Old public pages
* Certificate history
* Search-engine results

I compare dates carefully.

A domain may have changed owners, hosting providers or infrastructure over time.

So historical information needs especially careful attribution.

---

## 23. Build a Domain Map

I like to turn discoveries into a simple map:

```text
example.com
│
├── www.example.com
├── blog.example.com
├── docs.example.com
├── api.example.com
└── mail.example.com
```

Then I add public relationships:

```text
example.com
↓
Organization
↓
GitHub
↓
Public project
```

This makes the investigation much easier to understand.

---

## 24. Tools I Use

### DNS

```bash
dig
nslookup
host
```

### Passive subdomain discovery

```text
Subfinder
Amass
assetfinder
```

### Website fingerprinting

```text
WhatWeb
Wappalyzer
```

### HTTP inspection

```bash
curl
```

### Certificate research

```text
Certificate Transparency search
```

### Historical research

```text
Web archives
Historical DNS sources
```

I don't need every tool for every domain.

I choose the tool based on what I am trying to verify.

---

## 25. Basic Kali Setup

For the basic command-line tools:

```bash
sudo apt update
sudo apt install dnsutils curl whatweb
```

Check them:

```bash
dig -v
curl --version
whatweb --version
```

For tools such as Amass and Subfinder, use their current official installation instructions if the Kali package is unavailable or outdated.

---

## 26. My Practical Workflow

```text
Target
↓
Find public website
↓
Identify domain
↓
Confirm public association
↓
DNS lookup
↓
A / AAAA / MX / NS / TXT
↓
Passive subdomain discovery
↓
Certificate Transparency
↓
Search-engine queries
↓
Public GitHub references
↓
Technology identification
↓
Historical references
↓
Correlate
↓
Verify
↓
Document
```

---

## 27. What I Don't Do

I don't:

* Brute-force credentials
* Attempt to log into discovered services
* Exploit discovered services
* Bypass authentication
* Scan infrastructure without authorization
* Treat an IP as proof of someone's identity
* Treat a subdomain as proof of ownership
* Use leaked credentials
* Access private systems

This chapter is about **public domain and DNS intelligence**, not unauthorized exploitation.

---

# My Point of View

A domain is rarely just a website.

It can become a map of the public technical footprint.

One domain can lead to:

```text
Domain
↓
DNS
↓
Subdomains
↓
Certificates
↓
Public technologies
↓
Repositories
↓
Projects
↓
Organization
↓
Historical information
```

But the biggest mistake is assuming that every technical connection belongs to the same person.

A hosting provider isn't the owner.

An IP isn't a person.

A subdomain isn't automatically an organization.

A certificate isn't proof of control by a particular individual.

I separate **what I observed** from **what I believe it means**.

That's what keeps domain OSINT useful instead of turning it into a collection of assumptions.

---

# Final Rule

**Don't just find the domain. Map the public footprint around it.**

Start with the domain.

Follow the public DNS.

Find passive subdomains.

Check certificates.

Search the domain.

Find public projects.

Look at historical information.

Then correlate everything back to the original target.

**Domain → DNS → Subdomains → Certificates → Public Sources → Correlation → Verification → Documentation**
