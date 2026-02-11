# Reconnaissance

Reconnaissance is the initial step in a penetration test or security assessment, regardless of the methodology applied. Its purpose is to collect as much information as possible about a target—such as domains, IP ranges, network structure, technologies in use, and public-facing resources—without interacting directly or causing disruption (in passive reconnaissance) or with controlled interaction (in active reconnaissance).

## Pasive reconnaissance

Passive reconnaissance is the process of gathering information about a target without directly interacting with its systems. The goal is to collect as much data as possible from publicly available sources to understand the target’s infrastructure, technologies, and potential vulnerabilities without leaving any trace. Several methods can be applied to achieve this objective, such as OSINT.

### Types of public sources

Public sources are grouped according to their nature and the type of information they provide:

1. **Technical sources** - Provide information related to the digital infrastructure:

    - **WHOIS and RDAP records**: reveal ownership data, registration dates, and servers associated with domains.

    - **DNS records**: historical (A, MX, TXT, CNAME, NS) and current records help identify subdomains and relationships.

    - **Digital certificates**: Certificate Transparency repositories (crt.sh, censys.io) allow discovering active and old subdomains.

    - **Service search engines**: Shodan, Censys, ZoomEye, Fofa, or BinaryEdge facilitate the identification of exposed services and technical banners.

    - **Metadata in public documents**: PDFs, DOCX files, or images published by the organization may contain usernames, paths, or internal software information.

2. **Social and human sources** - Provide contextual and organizational information:

    - **Social and professional networks**: LinkedIn, Twitter/X, GitHub, or even Instagram can reveal employee names, internal structure, or technologies in use.

    - **Job postings**: often include specific software versions, frameworks, or architectures used.

    - **Public repositories and development platforms**: GitHub, GitLab, or Bitbucket are common sources of leaked credentials, configurations, and exposed secrets.

    - **Data breaches and leaks**: databases like HaveIBeenPwned, Dehashed, or Snusbase help identify previously compromised emails or passwords.

3. **Institutional and legal sources** - Provide information that, although public, can have strategic value:

    - **Corporate registries and official bulletins**: contain data about subsidiaries and technological partners.

    - **Annual reports, press releases, and public contracts**: useful for mapping suppliers, office locations, and technologies in use.

## Active reconnaissance

Active reconnaissance involves directly interacting with the target's systems or services to obtain more accurate information about its infrastructure, technologies, and configurations. Unlike passive reconnaissance, this process generates traffic to the analyzed assets, which can be distinguished from normal traffic by defensive mechanisms such as firewalls, IDS/IPS, or EDR.

Active reconnaissance aims to verify the existence and availability of assets discovered during passive reconnaissance, as well as to obtain information such as services, open ports, and running software versions.

### Common techniques and procedures

1. **DNS resolution and validation**: Direct queries to A, AAAA, MX, TXT, and NS records to verify domains.

2. **Ports and services scanning**: Detection of open ports with tools like Nmap, Masscan or Naabu. Identification of services and versions with NSE (Nmap Scripting Engine).

3. **Banner grabbing y fingerprinting**: Capturing service responses to determine exact versions, frameworks, or configurations (e.g., HTTP headers, SMTP messages, SSH banners, or FTP banners), using tools like curl, Netcat, Nmap, WhatWeb.

4. **Detection of technologies and frameworks**: Identifying CMS, libraries, and frameworks with tools such as Wappalyzer, BuiltWith, WhatRuns, or automated extensions of Burp Suite and ZAP.

5. **Surface Enumeration**: Initial identification of directories or endpoints using Gobuster, dirsearch, ffuf or wfuzz.