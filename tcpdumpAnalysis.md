# PCAP Analysis - 2021-09-14 Capture

## Overview

Analysis of a `.pcap` file containing a GET request to a spoofed executable, followed by investigation of the associated domains, IP addresses, and URL structure using `tcpdump` and VirusTotal.

## Initial Observation

A GET request was identified, made to what appears to be a spoofed executable (masquerading as `audiodg.exe`, a legitimate Windows Audio Device Graph Isolation process).

<img width="1379" height="269" alt="Screenshot From 2026-09-16 10-32-40" src="https://github.com/user-attachments/assets/7147903d-9121-44ab-907c-afbac4fd605c" />


The legitimate version of this file is a Microsoft application. A domain/IP lookup on the sending IP address confirmed that it is not owned by Microsoft, supporting the theory that this is a spoofed or impersonating file.

<img width="757" height="855" alt="Screenshot From 2026-09-16 10-39-00" src="https://github.com/user-attachments/assets/c174d440-9ca7-4484-bf05-7fbb755e86ce" />


The URL in the suspicious query points to the same address identified above.

### `tcpdump` Grep Results

<img width="1910" height="92" alt="Screenshot From 2026-09-16 10-46-11" src="https://github.com/user-attachments/assets/b12cae7c-5398-4412-9f51-1e4bf49bd84b" />


## Further Analysis

Command used:

```
tcpdump -tt -r 2021-09-14.pcap -A | grep ".audiodg.exe" -A500 | less
```

Results:

<img width="1130" height="257" alt="Screenshot From 2026-09-16 11-42-09" src="https://github.com/user-attachments/assets/246fb2d0-d75d-4901-857a-c2405a338e2a" />

A separate destination in the capture is a domain owned by Microsoft (likely Bing). The attacker may be using this domain to query information or to abuse it as part of a redirect chain toward the suspicious URL. This is currently a working theory and has not yet been confirmed - see notes below.

## URL Request Analysis

<img width="1147" height="510" alt="Screenshot From 2026-09-16 11-47-28" src="https://github.com/user-attachments/assets/9c58cb4c-92b6-47d0-ad09-1f3e80b2b760" />

- The URL was decoded and defanged as a best practice before documentation.
- The URL resolves directly to an IP address rather than a domain name - a notable red flag.
- The connection uses plain HTTP (not HTTPS).

## URL / File Reputation Analysis

### VirusTotal Results

<img width="1426" height="689" alt="Screenshot From 2026-09-16 11-50-11" src="https://github.com/user-attachments/assets/ccd89fa4-368c-46dd-8d7f-2fb129aadc06" />

### File Header Indicators

The typical header signature for a Windows executable (DOS header) is visible on the first line of the file content captured via `tcpdump`.

<img width="1116" height="130" alt="Screenshot From 2026-09-16 11-52-23" src="https://github.com/user-attachments/assets/234bf681-d9d1-4f31-931d-b7d8ca5aa686" />

Taken together, these indicators strongly suggest malicious intent.

## Next Steps

Extracting the file itself and generating hashes would require a tool such as Wireshark. This step will be carried out once I have a deeper working knowledge of the tool.

---
