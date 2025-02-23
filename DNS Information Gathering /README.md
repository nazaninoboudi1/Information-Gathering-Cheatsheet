#  DNS Information Gathering Cheat Sheet

## 📌 Introduction
DNS (Domain Name System) is a critical component of the internet, translating domain names into IP addresses. For security professionals, understanding how to gather DNS information is essential for reconnaissance in penetration testing and security assessments. This guide covers essential techniques and tools for **DNS enumeration and information gathering**.

---

## 🌍 Passive DNS Reconnaissance
Passive reconnaissance involves gathering information without direct interaction with the target.

### 🔍 WHOIS Lookup
Retrieve domain registration details:
```bash
whois target.com
```
Alternative services:
- [Whois Lookup](https://who.is/)
- [Domaintools WHOIS](https://whois.domaintools.com/)

### 🌎 DNS Record Lookup
```bash
dig target.com ANY +short
nslookup -type=ANY target.com
```
Alternative tools:
- `host -a target.com`
- `dnsrecon -d target.com`

### 🔎 Reverse DNS Lookup
Find domains pointing to a specific IP:
```bash
dig -x 192.168.1.1 +short
```
Alternative:
- `host 192.168.1.1`

### 🔥 Enumerate Subdomains (Passive)
```bash
subfinder -d target.com
assetfinder --subs-only target.com
```
Alternative tools:
- `crt.sh`
- `amass`
- `Sublist3r`

---

## 🚀 Active DNS Enumeration
Active reconnaissance involves direct interaction with the target, which may trigger security alerts.

### 🏴 Subdomain Brute-Forcing
```bash
gobuster dns -d target.com -w wordlist.txt
```
Alternative tools:
- `wfuzz`
- `amass enum -d target.com`

### 📜 Zone Transfer Attack
```bash
dig axfr @ns1.target.com target.com
```
Alternative:
- `dnsrecon -d target.com -t axfr`

### 🚀 Brute-Force DNS Records
```bash
dnsrecon -d target.com -t brt -D subdomains.txt
```

### 🕵️‍♂️ DNS Cache Snooping
```bash
dnschef --fakeip 192.168.1.100 --fakedomains target.com
```

### 📌 Identifying Wildcard DNS
```bash
dig random123.target.com
```
If the response is the same as `target.com`, the domain has a wildcard record.

---

## 🔑 DNS Security Checks
### 🔐 Checking SPF, DKIM, and DMARC Records
```bash
dig TXT target.com | grep "v=spf1"
dig TXT _dmarc.target.com | grep "v=DMARC1"
```
Alternative:
- `dmarcian.com/spf-survey/`

### 🕵️‍♂️ Detecting DNSSEC Configuration
```bash
dig +dnssec target.com
```

---

## 🎯 Online Tools
- [DNSDumpster](https://dnsdumpster.com/)
- [VirusTotal Passive DNS](https://www.virustotal.com/)
- [SecurityTrails](https://securitytrails.com/)
- [Shodan](https://www.shodan.io/)

---

## 🚀 Conclusion
This cheat sheet provides a **comprehensive guide for DNS reconnaissance** in penetration testing. DNS information gathering is a crucial phase in security assessments, and using these tools effectively can **reveal critical insights** about the target infrastructure.

**🔴 Remember: Always ensure you have permission before performing active reconnaissance!** 🚀
