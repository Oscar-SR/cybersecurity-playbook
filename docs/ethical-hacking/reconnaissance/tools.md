# Tools

## TLS certificates

TLS certificate analysis allows you to identify domain names and subdomains for which digital certificates have been issued. Certificates typically include additional information in the Subject Alternative Name (SAN) field, which lists the different hostnames associated with the same certificate. This information is especially useful for discovering less visible subdomains or internal services that, for operational reasons, also have public certificates.

### crt.sh

Website to consult public TLS certificate registries and obtain lists of associated domains and subdomains.

### Censys

Platform that indexes certificates, hosts, and associated metadata.

### CertSpotter

Monitoring service for new certificates issued for a domain.

### SSL Server Test

A tool designed for analyzing a server's TLS configuration, which also displays information about the certificate chain and visible extensions.

## DNS history

DNS history involves examining how DNS records and associated domains have changed over time, in order to identify assets that may have been visible in the past and that, although no longer in use, may still be accessible or misconfigured.

### SecurityTrails

It provides DNS history, associated IP ranges, temporary changes, and domain relationships.

### Farsight DNSDB

Database specializing in historical DNS records collected from multiple passive sources.

### ViewDNS

A suite of utilities for DNS queries, change analysis, WHOIS, and basic enumerations.

### RiskIQ PassiveTotal

Platform for correlating domains, associated infrastructure, and historical metadata.

## DNS delegations and transfers

DNS delegations make it possible to identify which name servers manage a domain and whether there are patterns indicating subdomains that are managed separately by external providers. This can reveal dependencies on third-party services or areas of the infrastructure that are managed independently.

On the other hand, DNS transfers (AXFR) are an operation through which a DNS server can deliver the complete list of records for a domain. Although in most current configurations this operation is blocked, it is important to understand it from a theoretical point of view, since when it is accidentally enabled it can expose sensitive information.

!!! warning "Warning"

    Its practical execution may involve direct interaction with the servers of the target domain.

### dig

It allows direct DNS queries, including attempting AXFR transfers when authorized.

```
dig +nocmd example.com A +noall +answer
dig +nocmd example.com AAAA +noall +answer
dig +nocmd example.com MX +noall +answer
dig +nocmd example.com TXT +noall +answer
dig +nocmd example.com ANY +noall +answer
```

### host

Simplified alternative for one-off DNS queries.

### dnsrecon

It allows you to identify DNS configurations, transfer attempts, and subdomains in combination with controlled resolutions.

```
dnsrecon -d example.com
```

### dnsenum

Automate DNS queries, subdomain resolution, and transfer testing when possible.

## Repositories

Code repositories and collaborative development platforms are a frequent source of information, especially when they are made public by mistake or when reusable components are shared. Repositories may contain: environment configurations, environment variables and API keys, commit histories that reveal changes in the infrastructure, and references to internal servers and paths.

### GitLeaks

It allows the detection of passwords, API keys, and other secrets embedded in repositories.

```
gitleaks detect --source . -v
```

### GitHub advanced search

It allows for precise searches by internal terms, files, and extensions.

## Cloud storage

The use of cloud storage services (such as Amazon S3, Google Cloud Storage, or Azure Blob Storage) can result in containers or buckets being configured as public, either by mistake or to facilitate temporary information sharing. When these containers are accessible without authentication, they may contain: downloaded backups or databases, configuration files and binary objects, images, activity logs, or internal reports.

### Google Dork

List public buckets by searching by domain name or organization name.

```
site:s3.amazonaws.com example.com
```

### S3Scanner

Identify publicly accessible buckets.

```
s3scanner -bucket bucket-name
```

```
s3scanner -bucket bucket-name -enumerate
```

### Grayhatwarfare public buckets

Collection of independent search engines focused on exposed buckets.

## Profiles and emails

### Hunter

Service to deduce construction patterns of corporate emails from domains.

```
hunter verify --email johndoe@apple.com | jq -r .data.score
```

```
hunter find --company example --full-name "John Doe" | jq -r .data.email
```

```
hunter search --domain example.com --department it | jq -r '.data.emails[] | "\(.value) \(.position)"'
```

```
hunter search --domain example.com --department it --offset 10 | jq -r '.data.emails[] | "\(.value) \(.position)"'
```

### Email Hippo

Tools designed to check the syntactic validity and existence of email addresses.

## Banners and metadata

Banners are messages that services display at the start of a connection, providing information such as software version, service type, or configuration. When these banners have been previously collected by search engines, it is possible to analyze them without establishing a direct connection.

### Shodan

A search engine specializing in connected devices, allowing filtering by port, technology, location, or manufacturer. Some search options include:

- `hostname:<string>` — match by hostname.
- `port:<n>` — filter by open port.
- `org:"Org Name"` — by organization.
- `product:"Apache httpd"` — by product detected in banner.
- `os:"Ubuntu"` — by detected operating system.
- `country:"US"` — by country.
- `city:"New York"` — by city.
- `http.title:"Example Page"` — by HTTP title.
- `ssl.cert.subject.CN:"example.com"` — by certificate CN.
- `ssl.cert.issuer.cn:"Let's Encrypt"` — by certificate issuer.
- `vuln:CVE-2021-XXXXX` — filter by known vulnerability.

### WhatWeb

Passive fingerprinting aimed at identifying web technologies through known signatures, when working on previously indexed information.

## Data breaches

Data breaches are a relevant source of information because they centralize leaked content, database fragments, credentials, or communications that have been disclosed publicly or semi-publicly. Analyzing these sources allows for the identification of whether email addresses, credentials, configurations, or sensitive fragments linked to an organization have appeared in past leaks, providing context about possible prior exposures and risk vectors.

### Have I Been Pwned

Source to check if emails associated with the organization have appeared in public leaks.

### Dehashed

Commercial database that allows searches by email, domain, hash, or username in large collections of leaks.

### Intelligence X

Intelligence platform that indexes pastes, documents, filtered databases, and underground network content.

### Snusbase

Search engine focused on correlating data in structured leaks.

### BreachDirectory

Similar services that aggregate and allow queries on filtered databases.

## ASN / netblocks / BGP

Analysis of ASNs (Autonomous System Numbers), IP ranges (netblocks), and BGP routing tables allows for understanding how an organization’s connectivity is structured. Autonomous systems define network blocks managed under a common routing policy. Knowing them helps to delineate the address space potentially associated with the target.

### Hurricane Electric BGP Toolkit

It provides information about ASNs, advertised prefixes, and associated routes.

### Team Cymru IP to ASN

Service to correlate IP addresses with ASNs and organizations.

### RADb

Routing log database used to query network assignments.

### PeeringDB

Platform that details routing relationships between providers and connected entities.

### RIPEstat

Analytics service that centralizes information on IP addresses and registered autonomous systems.