# Enumeration

Enumeration is the phase that follows reconnaissance within a penetration testing process, and it is, in fact, a subset of reconnaissance. While reconnaissance focuses on discovering and contextualizing assets or public information, enumeration seeks to extract detailed technical data directly from the discovered services by actively interacting with them.

During enumeration, the auditor analyzes each identified service or protocol looking for structured information that can be used later: users, shared resources, precise software versions, configurations, paths, policies, or even credentials. This stage requires direct interaction and generates activity visible to the target's monitoring systems.

## Types of Enumeration

### DNS (Domain Name System)

| Category      | Description |
|---------------|-------------|
| **What to look for** | Subdomains, A/AAAA/MX/TXT/CNAME records, delegations, historical records, and transferable zones (AXFR). |
| **Techniques** | Wordlist-based enumeration, controlled bruteforce, AXFR queries, Certificate Transparency searches, reverse resolution, and DNSSEC record validation. |
| **Tools** | `dig`, `dnsrecon`, `dnsenum`, `amass`, `subfinder`, `sublist3r`, `assetfinder`, `crt.sh` (Certificate Transparency), `massdns` (mass resolution), Chaos / SecurityTrails |
| **Tips** | Correlate subdomains with certificates and IP addresses to identify **forgotten assets** such as **staging environments, backups, or storage buckets**. |

### SMB / NetBIOS / Samba

| Category | Description |
|--------|-------------|
| **What to look for** | Shared resources, users, password policies, RPC pipes, SMB versions, null/guest sessions. |
| **Techniques** | Share enumeration, user enumeration (SMB enum), DCERPC pipe queries, SMB version and vulnerability checks (SMBv1/SMBv2/SMBv3). |
| **Tools** | `smbclient`, `enum4linux`, `rpcclient`, `smbmap`, Impacket (`smbclient.py`, `rpcdump`, `smbserver`), `crackmapexec`, Metasploit auxiliary modules. |
| **Tips** | Validate anonymous authentication and lockout policies; avoid massive brute force in production environments without authorization. |

### LDAP / Active Directory Enumeration

| Category | Description |
|--------|-------------|
| **What to look for** | Users, groups, GPOs, UPNs, trust relationships, domain controllers, exposed policies and configurations. |
| **Techniques** | Anonymous or authenticated LDAP queries, schema extraction, relationship enumeration, delegation and SPN discovery. |
| **Tools** | `ldapsearch`, `ldapdomaindump`, Impacket (`GetADUsers.py`), BloodHound (SharpHound / BloodHound-python), `ADRecon`, `CrackMapExec`, `PowerView`. |
| **Tips** | BloodHound greatly helps model privilege paths and plan privilege escalation. |

### SNMP

| Category | Description |
|--------|-------------|
| **What to look for** | Public/private SNMP communities, MIB tables (interfaces, routes), users, processes, software versions, configurations. |
| **Techniques** | SNMPv1/v2/v2c queries (read/write), SNMPv3 authentication attempts, MIB extraction. |
| **Tools** | `snmpwalk`, `snmp-check`, `onesixtyone`, `snmpenum`, Metasploit modules. |
| **Tips** | SNMPv1/v2 are unencrypted and may leak sensitive information; document and report if credentials are found. |

### Web & Directory Enumeration (HTTP/HTTPS)

| Category | Description |
|--------|-------------|
| **What to look for** | Endpoints, directories, sensitive exposed files, framework/CMS versions, parameters, and user entry points. |
| **Techniques** | Forced browsing (wordlists), parameter fuzzing, technology fingerprinting, header capture, cookie and session analysis, `robots.txt` and sitemap review. |
| **Tools** | `ffuf`, `gobuster`, `dirsearch`, `wfuzz`, Burp Suite, OWASP ZAP, `WhatWeb`, `Wappalyzer`, `Nikto` (basic recon), `EyeWitness`, `Aquatone`. |
| **Tips** | Limit requests and respect rate limits; use updated wordlists and correlate findings with SAST/SCA outputs. |

### APIs (REST / GraphQL)

| Category | Description |
|--------|-------------|
| **What to look for** | Exposed endpoints, schemas, sensitive parameters, undocumented endpoints, allowed methods, weak access control. |
| **Techniques** | Route enumeration, parameter fuzzing, OpenAPI/Swagger analysis, horizontal/vertical authorization testing, CORS and rate-limit checks. |
| **Tools** | Burp Suite (Intruder / Scanner / Extender), `ffuf`, Postman, Insomnia, `graphqlmap`, Nmap HTTP scripts. |
| **Tips** | Review public documentation and repositories to discover exposed specifications. |

### Users / Email / SMTP

| Category | Description |
|--------|-------------|
| **What to look for** | Account existence (VRFY/EXPN), open relay, authentication configurations, MTA versions, users leaked in emails or headers. |
| **Techniques** | SMTP banner grabbing, VRFY/EXPN tests, open relay verification, analysis of public email headers. |
| **Tools** | `swaks`, `smtp-user-enum`, `nmap --script smtp-*`, Metasploit modules (`smtp_enum`). |
| **Tips** | Many actions may generate spam or alerts; use carefully and only with authorization. |

### FTP / SFTP / Telnet

| Category | Description |
|--------|-------------|
| **What to look for** | Anonymous access, sensitive files, default accounts, versions and banners. |
| **Techniques** | Anonymous login, directory listing, file transfer, banner grabbing. |
| **Tools** | `ftp`, `lftp`, `curl`, `hydra` (if authorized) for authentication, Nmap scripts. |
| **Tips** | FTP transmits credentials in cleartext; document findings responsibly. |

### Databases (MSSQL, MySQL, PostgreSQL, Oracle)

| Category | Description |
|--------|-------------|
| **What to look for** | Open ports, default credentials, exposed client services, versions, configurations (e.g., `xp_cmdshell`, remote functions). |
| **Techniques** | Client connections, user/role enumeration, schema reading, privilege verification. |
| **Tools** | `sqlcmd`, `mysql`, `psql`, `sqsh`, `sqlmap` (for web apps), Nmap database scripts. |
| **Tips** | Destructive operations are forbidden unless authorized; limit actions to read-only where possible. |

### RPC / NFS / RSH / Rlogin

| Category | Description |
|--------|-------------|
| **What to look for** | NFS exports, exposed RPC services, remote share access, visible privileged accounts. |
| **Techniques** | `showmount`, `rpcinfo` queries, controlled mounting of exports (authorized environments only), remote user enumeration. |
| **Tools** | `rpcinfo`, `showmount`, `nfs-common`, legacy `rsh` / `rlogin` clients. |
| **Tips** | Many legacy services can be critical attack vectors in poorly patched environments. |

### Cloud Services & Storage (S3, GCS, Azure)

| Category | Description |
|--------|-------------|
| **What to look for** | Exposed buckets/object storage, misconfigured roles and permissions, public metadata, exposed serverless functions, leaked keys or secrets. |
| **Techniques** | Bucket permission checks (public-read/list), naming pattern enumeration, IAM policy analysis, review of public serverless functions. |
| **Tools** | `awscli`, `s3cmd`, `s3scanner`, `pacu` (AWS exploitation framework — extreme caution), `gcloud`, `az cli`, `ScoutSuite`, `Prowler`, `CloudMapper`. |
| **Tips** | Cloud testing requires special care due to shared scope and potential costs; clearly document scope and methods. |

### IoT / Banners / Exposed Services (Shodan-style)

| Category | Description |
|--------|-------------|
| **What to look for** | Devices with vulnerable firmware, exposed admin interfaces, cameras, routers, SCADA/OT systems with insecure services. |
| **Techniques** | Banner searching, port/service correlation, fingerprinting. |
| **Tools** | Shodan, Censys, ZoomEye, `masscan` for large-scale discovery, Nmap for verification. |
| **Tips** | Some devices may be critical to physical safety; avoid intrusive testing without explicit authorization. |

### Application & Dependency Enumeration (SCA / Supply Chain)

| Category | Description |
|--------|-------------|
| **What to look for** | Libraries with known vulnerabilities, secrets in repositories, outdated dependencies, artifacts in public registries. |
| **Techniques** | Public repository scanning, `package.json` / `requirements.txt` analysis, token searching in commits. |
| **Tools** | Snyk, Trivy, GitLeaks, Repo-Supervisor, Dependency-Track. |
| **Tips** | Supply-chain vulnerabilities and exposed secrets significantly accelerate escalation and risk validation. |

### Application-Specific Enumeration (Tomcat, Jenkins, Docker)

| Category | Description |
|--------|-------------|
| **What to look for** | Administrative panels, management endpoints, poorly protected containers, images containing credentials. |
| **Techniques** | Admin console access, default configuration review, orchestrator API enumeration. |
| **Tools** | Nmap, `curl`, `jenkins-cli`, Docker client (if access allowed), `kube-hunter` for Kubernetes (if in scope). |
| **Tips** | Administrative panels are highly sensitive; testing should be as non-disruptive as possible. |