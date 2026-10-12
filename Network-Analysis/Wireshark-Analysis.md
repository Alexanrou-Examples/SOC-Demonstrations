# Wireshark PCAP Analysis: Qakbot Malware Traffic:

### Overview:

Analysis of a `.pcap` file in Wireshark, starting with general capture statistics and progressing through HTTP, ARP, ICMP, SMTP, and SMB traffic to identify malware activity associated with the Qakbot malware family.

### Capture File Properties:

General information about the pcap file, gathered using the Capture File Properties statistics tool.

<img width="1372" height="870" alt="image" src="https://github.com/user-attachments/assets/93e79276-b1c1-4f7a-b44e-9a14adc56183" />

### IPv4 Traffic Overview:

IPv4 traffic sorted by packets from source A to destination B. The most packets are sent to an internal IP address at `10.0.0.6`, mostly just packets being sent to that address.

<img width="922" height="336" alt="image" src="https://github.com/user-attachments/assets/0a417617-9f38-416e-a7bc-bc45dac20ff4" />

### Protocol Hierarchy:

Notice the NetBIOS and the unencrypted HTTP packets, closer to the bottom of the hierarchy.

<img width="1556" height="760" alt="image" src="https://github.com/user-attachments/assets/e7447ffc-bec7-4621-a053-ff0038b339d3" />

### HTTP Traffic Analysis:

Further analysis of the HTTP packets.

#### Custom Columns:

<img width="1204" height="615" alt="image" src="https://github.com/user-attachments/assets/d7a1ddc7-0b5a-46e9-b4e2-02705c95ff72" />

- The Host value is an IP address instead of a domain name.
- A GET request is made to a `.dat` file, which is suspicious.

<img width="914" height="731" alt="image" src="https://github.com/user-attachments/assets/d273e0d8-eef5-488c-ba40-a0a9084dd923" />

#### Following the HTTP Request Stream:

<img width="845" height="712" alt="image" src="https://github.com/user-attachments/assets/a5f35793-156e-4df7-9e8c-e5e9eb96ced8" />

The traffic becomes increasingly suspicious:

- The user agent is `curl`, which is very unlikely to be a user unless they knowingly or unknowingly executed a script.
- Note the common string in the first line: "This program cannot be run in DOS mode".
- The magic byte at the start is for a DOS MZ executable (source: Google).

### HTTP request statistics also show this:

<img width="790" height="206" alt="image" src="https://github.com/user-attachments/assets/4ce0182d-e49b-4550-9255-2b52dbb386f9" />

#### File Export and Reputation Checks:

Exported the file for further analysis.

<img width="831" height="144" alt="image" src="https://github.com/user-attachments/assets/cdc7073e-a55c-4478-b020-52ace4bf429a" />

The hash value was used to check the score on VirusTotal and similar tools.

**VirusTotal:**

<img width="1451" height="528" alt="image" src="https://github.com/user-attachments/assets/f65cdb16-1bec-4424-840a-8ac8d7aabe54" />

**MalwareBazaar:**

<img width="1274" height="137" alt="image" src="https://github.com/user-attachments/assets/6ed08b71-1316-44e6-b17c-0169015083fb" />

The file seems to be a part of the Qakbot malware family.

### Malware Behavior Research:

Further research on the malware itself, to check for other endpoints that could be affected or whether the malware has been executed:

- The goal seems to be to use ARP as a way to gather information about other endpoints.
- Uses SMB to spread across the network.
- Exfiltrates emails for a sophisticated thread hijacking attack.

#### ARP Packets:

Looking at the ARP packets in the pcap file:

<img width="1338" height="338" alt="image" src="https://github.com/user-attachments/assets/50b16f75-15da-4606-bd8a-be8f8bfac9cb" />

The requests are sequential, checking whether hosts are alive in order to find another endpoint to test.

#### ICMP Requests:

Filtered for ICMP requests to check who responded:

<img width="1243" height="124" alt="image" src="https://github.com/user-attachments/assets/b8ad8a83-fe9a-40d9-8561-db86d0ee0595" />

Probe requests to one of the IP addresses:

<img width="1781" height="469" alt="image" src="https://github.com/user-attachments/assets/c685ea04-2fe5-454b-b02f-b33377f24b5f" />

### SMTP Traffic:

<img width="824" height="703" alt="image" src="https://github.com/user-attachments/assets/b18a091c-0952-46f2-bbd5-003dceedb827" />

Decoded values:

<img width="1019" height="467" alt="image" src="https://github.com/user-attachments/assets/f7fa3118-5c18-4489-87a6-84a2333fbbe8" />

In this case the authentication failed, but the information could lead to further actions since the account information might have been compromised. This is my observational assumption without proof, since the decoded values include a username and password.

### SMB Traffic:

<img width="1254" height="368" alt="image" src="https://github.com/user-attachments/assets/e0e4586c-6506-4416-8efe-db7a9c28f75f" />

- In an AD environment, `gpt.ini` files are common.
- The DLL files are suspicious. It might be a Windows update going out, but since the naming conventions are random, it does raise red flags.

Exporting the files and looking at the hashes:

<img width="1096" height="193" alt="image" src="https://github.com/user-attachments/assets/4c0fee75-3c5b-4966-8c13-91c9d93a8135" />

- Duplicate hashes were found in different DLL files.
- The hash is also the same as the malware file in the previous analysis screenshot.

### Next Steps:

Direct your attention to the affected endpoint, in this case the domain controller.
