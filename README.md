# Penetration Testing Practical Report – Week 02

**Author:** Akash P  
**Program:** Networkwalks Cybersecurity Internship  
**Activities:** Public-source reconnaissance with TheHarvester and local network discovery with Zenmap  
**Report:** [`report/Akash_P_Penetration_Testing_Report_Week2.docx`](report/Akash_P_Penetration_Testing_Report_Week2.docx)

## Overview

This repository contains my Week 02 practical documentation and supporting evidence. The work is divided into two activities:

1. **OSINT reconnaissance:** Used TheHarvester 4.11.1 to collect publicly indexed host, IP, email, URL and ASN information for the domain entered in the command.
2. **Local network discovery:** Used Zenmap/Nmap to perform a ping scan against the lab subnet `10.0.0.0/24` and identify responding hosts.

The purpose of the exercise was to understand the type of information that can be collected during reconnaissance, interpret tool output carefully, and document a basic network discovery process.

## Repository Structure

```text
Akash-P-Penetration-Testing-Report/
├── README.md
├── report/
│   └── Akash_P_Penetration_Testing_Report_Week2.docx
├── evidence/
│   ├── screenshots/
│   │   ├── theharvester-all-sources.png
│   │   ├── theharvester-results-summary.png
│   │   ├── theharvester-baidu-results.png
│   │   └── zenmap-local-ping-scan.png
│   └── topology/
│       └── local-network-topology.pdf
└── raw-output/
    ├── theharvester-all-sources.txt
    └── theharvester-baidu.txt
```

## Tools and Environment

| Tool | Use |
|---|---|
| Kali Linux | Environment used for TheHarvester |
| TheHarvester 4.11.1 | Public-source information gathering |
| Zenmap / Nmap 7.99 | Local subnet host discovery |
| Baidu source | Secondary TheHarvester query |

## Commands Executed

### 1. TheHarvester – multiple sources

```bash
theHarvester -d microsoft.com -l 50 -b all
```

The run reported 9 ASNs, 8 interesting URLs, 166 IP addresses, 3 email addresses and 9,973 hostnames. The output also showed that several integrations could not run because API credentials were missing or invalid.

### 2. TheHarvester – Baidu source

```bash
theHarvester -d microsoft.com -l 1000 -b baidu
```

This query returned no IP addresses, emails, people or hosts.

### 3. Zenmap – local network ping scan

```bash
nmap -sn 10.0.0.0/24
```

The scan covered 256 addresses and reported two live hosts:

- `10.0.0.1`
- `10.0.0.2`

The supplied Zenmap output displayed MAC address `52:54:00:12:35:00` for `10.0.0.1` (QEMU virtual NIC). A MAC address for `10.0.0.2` was not visible in the supplied screenshot, so it is not stated here.

## Key Observations

- TheHarvester results depend on the selected sources and the availability of their API credentials.
- Aggregated hostname and IP results should be validated before being treated as a current asset inventory.
- A host responding to a ping scan is not, by itself, evidence of a vulnerability.
- The local scan found two responding hosts in the `10.0.0.0/24` lab subnet.
- The evidence supplied did not include a separate `ipconfig` or `ip addr` output for the tester's own interface address.

## Authorization and Scope Note

The supplied Networkwalks Letter of Authorization (reference `NW-LOA-B082-017`) identifies `networkwalks.com` and the tester's own LAN as the authorized targets. The recorded TheHarvester commands in this repository queried `microsoft.com`, which is not listed in that letter. That query is documented transparently as a separate public-source OSINT exercise and must not be represented as testing authorized by Networkwalks. The Zenmap scan was performed against the local lab subnet.

Only perform reconnaissance or scanning on systems for which you own the environment or have explicit permission. No exploitation, brute-force activity, denial-of-service testing or access to private data is documented in this project.

## Evidence

Screenshots are stored in [`evidence/screenshots/`](evidence/screenshots/), the topology export is in [`evidence/topology/`](evidence/topology/), and the supplied terminal outputs are in [`raw-output/`](raw-output/).

## Learning Outcomes

- Practised collecting publicly indexed information using TheHarvester.
- Observed how missing API keys affect the completeness of OSINT collection.
- Compared results from an aggregated source run and a single-source query.
- Used Zenmap to identify live devices on a local subnet.
- Learned to distinguish raw tool output from verified security findings and to document scope limitations.

---

**Author:** Akash P  
**Project:** Networkwalks Cybersecurity Internship – Week 02  
