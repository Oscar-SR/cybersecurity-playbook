# Tools

## Wordlists

A wordlist is a file containing words or paths that fuzzing/discovery tools use as inputs to test URLs, hostnames, parameters, or credentials.

### SecLists

Large collection organized by categories (directories, vhosts, params, usernames, passwords). Usual Linux path: `/usr/share/seclists/`

### DirBuster wordlist

Lists designed for forced browsing (small/medium/large).

### FuzzDB

Payloads and specific routes for application fuzzing and attacks.

### rockyou.txt

Classic list of passwords for brute-force testing. Usual Linux path: `/usr/share/wordlists/rockyou.txt.gz`

## Web fuzzing

Web fuzzing is a security testing technique used to discover vulnerabilities in web applications by automatically sending a large number of unexpected or random inputs to different parts of a website, such as URLs, form fields, headers, or parameters. The goal is to trigger errors, misconfigurations, or unintended behavior that could indicate security issues, such as SQL injection, cross-site scripting (XSS), file inclusion, or broken access controls. By systematically “fuzzing” the application with a variety of payloads, testers can identify weak points that may be exploitable, helping to improve the overall security and resilience of the web application.

### Gobuster

```
gobuster dir -u https://example.com -w /usr/share/wordlists/dirb/common.txt
```

### Ffuf

Ffuf uses the concept of `FUZZ`, which is a marker that Ffuf replaces with words from the wordlist.

```
ffuf -u https://example.com/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt
```

## Virtual host discovery

Many servers and load balancers host multiple sites on the same IP address (virtual hosting); by varying the Host header with potential names (subdomains generated through permutation, names extracted from CT logs, or specific wordlists), the server may respond with different content or reveal the existence of virtual hosts that are not publicly indexed. This technique helps validate whether certain hostnames are served by the same IP server or whether specific configurations exist for particular hostnames.

### Gobuster

```
gobuster vhost -u https://example.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

### Ffuf

```
ffuf -u http://127.0.0.1/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million5000.txt -H "Host: FUZZ.example.com"
```

## Live host detection

Live host detection aims to identify which IP addresses within a range or list respond to network queries. This can be done in several ways: using ICMP requests (ping), TCP/UDP probes to common ports, ARP queries on local networks, or checking HTTP headers for web hosts. The goal is to narrow down the set of addresses for more detailed analysis, optimizing time and reducing impact.

### ping

Simple response check from an IP address.

```
ping -c 4 1.2.3.4
```
```
ping -c 10 -i 0.2 host.example.com
```

### arp-scan

Discover devices on the local network using ARP.

```
sudo arp-scan --localnet
```
```
sudo arp-scan -I eth0 192.168.1.0/24
```
```
sudo arp-scan --retry=3 --timeout=200 -I wlan0 10.0.0.0/24
```

### masscan

It can be used to detect hosts quickly, taking care in setting the speed.

```
masscan 192.168.1.0/24 -p0-65535 --rate=1000 -oX masscan.xml
```
```
masscan 10.0.0.0/8 -p80,443 --rate=500 -oG masscan_grep.txt
```
```
masscan --ping-only 203.0.113.0/24 --wait 3 --rate=1000
```

### nmap

It supports multiple detection methods (ICMP, TCP SYN, ACK probes, etc.) and is widely used for its versatility.

```
nmap -sn 192.168.1.0/24
```
```
nmap -sn -PE -PA21,22,23,80 10.0.0.0/24
```
```
nmap -sn -PS443 -PA80,3389 -oA nmap_ping_scan 203.0.113.0/24
```
```
nmap -sn -PR 192.168.0.0/24
```
```
nmap -Pn -n --host-timeout 30s -oA nmap_no_ping 198.51.100.0/24
```

## Port scanning

Port scanning aims to identify which TCP/UDP ports are open on detected hosts, which in turn suggests which services are available. Multiple scanning techniques exist that balance speed, accuracy, and detectability: SYN scan (half-open), connect scan, UDP scan, and stealthier scans that fragment packets or modulate timing.

### nmap

Reference tool for port scanning and service detection, supporting multiple techniques (SYN, connect, UDP), scripting (NSE), and export in XML/JSON formats.

### masscan

Extremely fast scanner for large address ranges; its use requires strict speed and segmentation control to avoid saturation.

## TLS and HTTP fingerprinting

TLS and HTTP fingerprinting focuses on analyzing the parameters of the secure transport layer (TLS) and the HTTP headers exposed by web servers and proxies. In TLS, elements such as the certificate chain, cipher parameters, extensions, and supported versions provide signals about the underlying implementation and architecture (for example, CDNs, TLS terminators, or proxies). In HTTP, headers (Server, X-Powered-By, HSTS, CSP, cookies) make it possible to infer web servers, frameworks, and security practices.

### OpenSSL

It allows you to establish TLS connections and view the certificate chain and encryption parameters.

```
openssl s_client -connect example.com:443 -servername example.com
```
```
openssl s_client -connect example.com:443 -showcerts -servername example.com
```
```
openssl s_client -connect example.com:443 -tls1_2 -cipher 'ECDHE-RSAAES128-GCM-SHA256' -servername example.com
```
```
openssl x509 -in cert.pem -noout -text
```
```
openssl s_client -connect example.com:443 </dev/null 2>/dev/null | openssl
```
```
x509 -noout -text | sed -n '/Subject:/,/X509v3/{p}'
```

### sslyze

Tool for examining TLS server features, ciphers, and vulnerabilities related to the TLS layer.

```
sslyze --regular example.com:443
```
```
sslyze --certinfo=basic example.com:443
```
```
sslyze --compression --reneg --sslv2 --sslv3 --heartbleed example.com:443
```
```
sslyze --tlsv1_3 --tlsv1_2 --tlsv1_1 --tlsv1 example.com:443
```

### testssl.sh

It provides a detailed analysis of TLS configurations and compatibility.

```
testssl.sh --fast example.com:443
```
```
testssl.sh --openssl=openssl --logfile testssl_examplecom.log example.com:443
```
```
testssl.sh --warnings --sslv2 --sslv3 --heartbleed --tls1 example.com:443
```

### curl

It allows you to obtain HTTP headers and verify responses, redirects, and session cookies.

```
curl -I https://example.com
```
```
curl -v --insecure https://example.com
```
```
curl -sS -D - -o /dev/null https://example.com
```
```
curl -L -I -H "User-Agent: Mozilla/5.0" https://example.com
```
```
curl -I -H "Accept-Encoding: gzip,deflate" https://example.com
```

## Web technology fingerprinting

Web technology fingerprinting aims to identify frameworks, content management systems (CMS), libraries, application servers, and auxiliary components that make up an application’s technology stack. This information is valuable for technology mapping and for designing laboratory exercises focused on specific configurations.

### WhatWeb

Tool for identifying web technologies based on patterns and signatures in HTTP responses.

### Wappalyzer

Identifies frameworks, libraries, and services based on headers and resources loaded by the page.

### BuiltWith

Platform for identifying providers, CMS and technologies used by a website.

## API enumeration

APIs represent interaction surfaces where resources and operations are exposed. Endpoint enumeration aims to identify routes, supported HTTP methods (GET, POST, PUT, DELETE, OPTIONS), expected parameters, and, when possible in passive mode, the presence of self-documented descriptors (OpenAPI/Swagger, WADL).

### Burp Suite

Tool for crawling, endpoint discovery, traffic capture and analysis.

### Postman

Exploration and manual testing of APIs.

## Shared resources and permissions

Shared resources (SMB folders, NFS shares, exposed web resources, cloud buckets) and their permissions are key elements for understanding an organization’s effective exposure surface. Enumeration aims to identify which resources are available, what apparent permissions exist, and whether it is possible to list contents without credentials. In an academic context, inspection focuses on metadata and visible listings or is performed using tools that do not modify the resources.

### smbclient

### showmount

### rclone

### enum4linux