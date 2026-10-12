# PCAP Challenge: Pikabot Malware and DNS Tunneling:

### Overview:

Analysis of a `.pcap` file involving a malicious file download disguised as an image, followed by identification of DNS tunneling activity consistent with the Pikabot malware family.

### Capture File Properties:

<img width="1275" height="853" alt="image" src="https://github.com/user-attachments/assets/9e2874d6-bc56-42ae-b090-14cc15e99812" />

### Domain Resolution:

Associated IP address of the domain name:

<img width="1598" height="89" alt="image" src="https://github.com/user-attachments/assets/ae5d359a-8b2d-4719-b879-f7f6aa596d44" />

### HTTP Traffic:

Total HTTP packets:

<img width="1062" height="567" alt="image" src="https://github.com/user-attachments/assets/50ad54f3-84e6-4f74-a98a-7e3323aad48e" />

Relative path accessed on the web server to request a file for download:

<img width="1380" height="109" alt="image" src="https://github.com/user-attachments/assets/062e18d3-8db2-4399-beac-90298e80e1b4" />

#### File Type Mismatch:

- **Claimed file type:** `image/gif`

<img width="1380" height="109" alt="image" src="https://github.com/user-attachments/assets/b8044d69-e38c-432d-a186-6e62f71f12d4" />

- **Actual file type:** `MZ`

<img width="732" height="289" alt="image" src="https://github.com/user-attachments/assets/f9e3c660-2479-448b-b217-73e53f02c64a" />

### Download Method:

Command-line utility used to download the file: **PowerShell**.

<img width="823" height="295" alt="image" src="https://github.com/user-attachments/assets/d8ce6d60-4878-40d9-8401-881a4cbae3bb" />

### File Hash:

**SHA256:** `9b8ffdc8ba2b2caa485cca56a82b2dcbd251f65fb30bc88f0ac3da6704e4d3c6`

<img width="976" height="76" alt="image" src="https://github.com/user-attachments/assets/28855077-97cf-4aad-b452-6f623d526d0d" />

### VirusTotal Results:

- **Conclusion:** Malicious
- **Type of malware:** Trojan
  - `Trojan.Agent.Pikabot`

<img width="1517" height="595" alt="image" src="https://github.com/user-attachments/assets/e94d873b-ef57-4aef-b899-a7f1b5fb7faf" />

### DNS Traffic:

The majority of UDP packets are DNS protocol traffic.

<img width="1709" height="274" alt="image" src="https://github.com/user-attachments/assets/63b0ba3f-6619-42f1-9b46-4e0364d25840" />

Base domain that is continuously queried: `steasteel[.]net`


### MITRE ATT&CK Mapping:

- **Technique ID:** T1071.004 (Application Layer Protocol: DNS)
- The PCAP file is known as DNS tunneling.

<img width="1322" height="625" alt="image" src="https://github.com/user-attachments/assets/47b1c6fa-c161-4c40-a6e8-c91fb4d46ae5" />
