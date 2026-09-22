# Wireshark PCAP Analysis - Qakbot Malware Traffic

## Overview

Analysis of a `.pcap` file in Wireshark, starting with general capture statistics and progressing through HTTP, ARP, ICMP, SMTP, and SMB traffic to identify and confirm malware activity later attributed to the Qakbot family.

## Capture File Properties

General information about the pcap file, gathered using Wireshark's Capture File Properties statistics tool.

<img width="1372" height="870" alt="Screenshot From 2026-09-22 11-52-45" src="https://github.com/user-attachments/assets/1dacbb18-cf89-4ff2-b3fd-7733d7f054bd" />

## IPv4 Traffic Overview

IPv4 traffic sorted by packet count from source A to destination B. The highest packet count is directed at an internal IP address, `10.0.0.6` ; mostly one directional traffic being sent to that address.

<img width="922" height="336" alt="Screenshot From 2026-09-22 11-53-49" src="https://github.com/user-attachments/assets/2cbd3b11-d3ca-4bc1-ad57-07c84af10ca0" />

## Protocol Hierarchy

Notable presence of NetBIOS and unencrypted HTTP traffic, visible further down the protocol hierarchy.

<img width="1556" height="760" alt="Screenshot From 2026-09-22 11-58-22" src="https://github.com/user-attachments/assets/396d6930-e9b7-4785-9fc2-43b2ffe6b44f" />

## HTTP Traffic Analysis

### Custom Columns

<img width="1204" height="615" alt="Screenshot From 2026-09-22 12-02-57" src="https://github.com/user-attachments/assets/3817566a-95b9-410b-b4b7-3dfcc9cfdf46" />

- The `Host` value is an IP address rather than a domain name.
- A GET request is made to a `.dat` file; suspicious behavior.

<img width="914" height="731" alt="Screenshot From 2026-09-22 12-04-34" src="https://github.com/user-attachments/assets/629914a1-0bf9-440b-a675-641f2169cb57" />

### Following the HTTP Request Stream

<img width="845" height="712" alt="Screenshot From 2026-09-22 12-07-00" src="https://github.com/user-attachments/assets/207fadd7-d4e0-4b86-bb35-6d9fd4c5b339" />

Several indicators increase the suspicion level here:
- The `User-Agent` is `curl`, which is very unlikely for a genuine user request — this typically indicates a script being executed, knowingly or unknowingly, on the host.
- The response contains the familiar string `"This program cannot be run in DOS mode."`
- The response begins with the "MZ" magic byte signature, indicating a DOS/Windows executable (source: general research).

HTTP request statistics further support this:

<img width="790" height="206" alt="Screenshot From 2026-09-22 12-18-07" src="https://github.com/user-attachments/assets/47377070-2726-491a-a9fe-be91e440c0e9" />

### File Export and Reputation Checks

The suspicious file was exported from the capture for further analysis.

<img width="831" height="144" alt="Screenshot From 2026-09-22 12-21-06" src="https://github.com/user-attachments/assets/871c7298-ace9-4585-8ef1-58e054b87de5" />

The resulting hash was checked against file reputation services:

**VirusTotal:**

<img width="1451" height="528" alt="Screenshot From 2026-09-22 12-22-57" src="https://github.com/user-attachments/assets/2d1df336-6e39-4a5b-856a-8c1f7dd7e980" />

**MalwareBazaar:**

<img width="1274" height="137" alt="Screenshot From 2026-09-22 12-25-30" src="https://github.com/user-attachments/assets/5283c191-108e-416a-a680-757d92f3736d" />

Results indicate the file is associated with the Qakbot malware family.

## Malware Behavior Research

Further research into Qakbot's behavior was carried out to check for other affected endpoints and to determine whether the malware had executed successfully. Key behaviors identified:

- Uses ARP as a reconnaissance method to gather information about other endpoints on the network.
- Uses SMB to spread laterally across the network.
- Exfiltrates emails to support a sophisticated thread-hijacking attack.

### ARP Traffic

<img width="1338" height="338" alt="Screenshot From 2026-09-22 12-30-49" src="https://github.com/user-attachments/assets/10d91e12-a737-424b-a2a7-1e0372577e17" />

The ARP requests are sequential, consistent with the malware probing to check which hosts are alive in order to identify additional endpoints to target.

### ICMP Traffic

Filtered for ICMP requests to identify which hosts responded to the probes.

<img width="1243" height="124" alt="Screenshot From 2026-09-22 12-32-50" src="https://github.com/user-attachments/assets/2ba230f3-3385-41d6-828b-670b34da9a86" />

Probe requests directed at one of the identified IP addresses:

<img width="1781" height="469" alt="Screenshot From 2026-09-22 12-43-48" src="https://github.com/user-attachments/assets/cdbde55f-df5f-4fd7-a636-c7d8688d8641" />

### SMTP Traffic

<img width="824" height="703" alt="Screenshot From 2026-09-22 12-44-35" src="https://github.com/user-attachments/assets/957759e4-84f1-41e9-a09e-b3c646a97f0f" />

Decoded values:

<img width="1019" height="467" alt="Screenshot From 2026-09-22 12-46-07" src="https://github.com/user-attachments/assets/0d3ab318-c515-4c8a-8933-c6e8f7a709dc" />

In this instance, authentication failed. However, the decoded data includes a username and password, so the associated account credentials should be treated as potentially compromised. *(Note: this is an observational assumption based on the presence of credentials in the traffic, not confirmed proof of compromise.)*

### SMB Traffic

<img width="1254" height="368" alt="Screenshot From 2026-09-22 12-50-13" src="https://github.com/user-attachments/assets/1d548564-d152-420b-863f-a23ac09680a2" />

`gpt.ini` files are commonly present in an Active Directory environment. The accompanying `.dll` files are suspicious ; while this pattern could resemble a legitimate Windows update being pushed out, the randomized naming convention raises red flags.

Exporting the files and reviewing their hashes:

<img width="1096" height="193" alt="Screenshot From 2026-09-22 12-53-32" src="https://github.com/user-attachments/assets/fb1fc4e4-c56d-4132-b9e3-ef1422124ca5" />

- Duplicate hashes were found across different `.dll` files.
- One of these hashes also matches the malware file identified earlier in this analysis.

## Next Steps

Focus further investigation on the affected endpoint - in this case, the domain controller.
