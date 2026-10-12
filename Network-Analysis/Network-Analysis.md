### PCAP Analysis
### Overview

Analysis of a .pcap file containing a GET request to a spoofed executable, followed by investigation of the associated domains, IP addresses, and URL structure using tcpdump and VirusTotal.

### Initial Observation

A GET request was identified, made to what appears to be a spoofed executable (audiodg.exe).

<img width="1379" height="269" alt="image" src="https://github.com/user-attachments/assets/516f7f85-961c-49c5-a5c3-dd9f1a4d572b" />

The legitimate version of this file is a Microsoft application. A domain lookup on the sender's IP address verified that the IP is not owned by Microsoft.

<img width="757" height="855" alt="image" src="https://github.com/user-attachments/assets/45df8baf-009f-412c-9410-d881959c6270" />

The URL in the suspicious query points to the same address identified above.

### tcpdump Grep Results

<img width="1910" height="92" alt="image" src="https://github.com/user-attachments/assets/2a5dcb6e-67ed-4e93-afc0-3fc31b5c308d" />

### Further Analysis

Command used:

bash
tcpdump -tt -r 2021-09-14.pcap -A | grep ".audiodg.exe" -A500 | less

Results:

<img width="1130" height="257" alt="image" src="https://github.com/user-attachments/assets/6ac90274-0904-4f6f-881e-e05c0fcba26d" />

The destination is a domain owned by Microsoft, likely Bing. The attacker is most likely using it in some way, either to query information or to abuse it to redirect to the suspicious URL.

### URL Request Analysis

<img width="1147" height="510" alt="image" src="https://github.com/user-attachments/assets/0136a245-b730-4a00-be0e-e9f0c8eae02f" />

The URL was decoded and defanged as a best practice.
The URL points to an IP address instead of a domain name, which is very suspicious.
The request uses plain HTTP.
URL / File Analysis
VirusTotal Results

<img width="1426" height="689" alt="image" src="https://github.com/user-attachments/assets/69aee2c6-8232-4a09-af78-1ae17428b48f" />

### File Header Indicators

The typical header for Windows executables (the DOS header) is visible in the first line of the file content displayed by tcpdump.

<img width="1116" height="130" alt="image" src="https://github.com/user-attachments/assets/3bca24d4-a9f0-4d20-b534-659d4d13ee3f" />

A significant amount of evidence suggests the file has malicious intent.

Next Steps

Extracting the file and examining its hashes requires a tool such as Wireshark. This will be done once I have a deeper working knowledge of the tool.
