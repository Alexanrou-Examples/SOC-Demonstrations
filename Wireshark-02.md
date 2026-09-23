# PCAP Challenge - Pikabot Malware & DNS Tunneling

## Overview

Analysis of a `.pcap` file involving a malicious file download disguised as an image, followed by identification of DNS tunneling activity consistent with the Pikabot malware family.

## Capture File Properties

<img width="1275" height="853" alt="Screenshot From 2026-09-23 10-56-50" src="https://github.com/user-attachments/assets/c02a2790-ddda-46b3-8055-29a145c3854e" />

## Domain Resolution

Associated IP address for the domain name in question.

<img width="1598" height="89" alt="Screenshot From 2026-09-23 11-08-30" src="https://github.com/user-attachments/assets/3c5d0968-0d1a-4c83-ac16-3181bfdbc3da" />

## HTTP Traffic

Total HTTP packets observed in the capture:

<img width="1062" height="567" alt="Screenshot From 2026-09-23 11-10-06" src="https://github.com/user-attachments/assets/35af5aaa-9f70-4224-8b4c-8dafb5fbafbb" />

Relative path accessed on the web server to request a file for download:

<img width="1380" height="109" alt="Screenshot From 2026-09-23 11-11-24" src="https://github.com/user-attachments/assets/3913385c-8db9-4012-8de1-897a174d2578" />

### File Type Mismatch

- **Claimed file type (per HTTP response):** `image/gif`
<img width="1380" height="109" alt="Screenshot From 2026-09-23 11-12-26" src="https://github.com/user-attachments/assets/73aa7d9a-deb2-4eb3-8a46-35371a3cb00a" />

- **Actual file type:** `MZ` (Windows/DOS executable signature)


<img width="732" height="289" alt="Screenshot From 2026-09-23 11-13-26" src="https://github.com/user-attachments/assets/59c57e96-03a4-4f1b-abc8-5596b9e6e50e" />

## Download Method

Command-line utility used to download the file: **PowerShell**.

<img width="823" height="295" alt="Screenshot From 2026-09-23 11-16-15" src="https://github.com/user-attachments/assets/8968921c-6d59-4708-a66d-824577576f5a" />

## File Hash

**SHA256:** `9b8ffdc8ba2b2caa485cca56a82b2dcbd251f65fb30bc88f0ac3da6704e4d3c6`

<img width="976" height="76" alt="Screenshot From 2026-09-23 11-20-24" src="https://github.com/user-attachments/assets/bc92baec-dc05-43cb-b2ba-ac461633d8d5" />

## VirusTotal Results

- **Conclusion:** Malicious
- **Malware type:** Trojan
- **Classification:** `Trojan.Agent.Pikabot`
<img width="1517" height="595" alt="Screenshot From 2026-09-23 11-22-49" src="https://github.com/user-attachments/assets/5858acb1-03d4-4871-83f4-828b24f471a5" />

## DNS Traffic

The majority of UDP packets in the capture are DNS protocol traffic.


Base domain continuously queried throughout the capture: `steasteel[.]net`

<img width="1709" height="274" alt="Screenshot From 2026-09-23 11-24-12" src="https://github.com/user-attachments/assets/5a865d17-7a88-43e4-9c12-67cd47129ce5" />

## MITRE ATT&CK Mapping

- **Technique ID:** T1071.004 - Application Layer Protocol: DNS
- This PCAP is consistent with known DNS tunneling behavior.

<img width="1322" height="625" alt="Screenshot From 2026-09-23 11-29-18" src="https://github.com/user-attachments/assets/9bb68b8d-6279-4104-a63d-b8cc0591fc4f" />
