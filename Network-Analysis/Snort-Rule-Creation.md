# Snort Rule Creation

### Overview

A collection of custom Snort rules written and tested against packet captures, covering ICMP alerting, malicious executable downloads, user agent detection, SSH brute force detection, and a web server attack challenge involving LFI and brute force activity.

### Basic Alert Rule: ICMP to 8.8.8.8

Created an alert rule that sends an alert to the console each time its conditions are met. In this case, the conditions are met if ICMP traffic to `8.8.8.8` is detected from any source IP address or port, and Snort then raises an alert. For ease of use, the console argument was used to get a live reading.

**SIEM integration and other output methods:**

- To use other output methods with a SIEM, Snort can be configured to output alerts to syslog, and the SIEM can then be integrated to capture the syslog.
- With Wazuh, this requires configuring the `ossec.conf` file on the agent or manager, then:
  - Creating a custom decoder
  - Creating the rule
- Wazuh also has integrated notification capabilities.
- For email alerting using Snort alone, `alert_fast` can be used together with a bash script that sends the alert as an email.

<img width="1119" height="508" alt="image" src="https://github.com/user-attachments/assets/294ccef6-ea9b-4bbf-91c6-326d46ca6085" />

### Raw Packet Logs for SIEM Ingestion

Raw packet logs can be dynamically forwarded into the SIEM, allowing alerts to be created on the dashboard.

<img width="1117" height="211" alt="image" src="https://github.com/user-attachments/assets/52c8c27d-4a52-4238-b104-dcc897a60c26" />

### Rule: Alert on .exe File Download

Created a rule to generate an alert when a `.exe` file is downloaded.

<img width="1033" height="215" alt="image" src="https://github.com/user-attachments/assets/143fb30e-8e16-4473-929c-ebea303fbf67" />

### The decoded log file shows the rule was successful:

<img width="796" height="443" alt="image" src="https://github.com/user-attachments/assets/8cc265ed-a6b7-4eef-aab6-0f8e67f1ea2a" />

### Additional Precautions: Missing .exe File Extension

To account for cases where the `.exe` file extension is not present, the stream of the malicious `.exe` file was followed in the pcap file using Wireshark.

<img width="687" height="204" alt="image" src="https://github.com/user-attachments/assets/a39a0f3f-c5cc-4c3d-bb44-62d70a478bec" />

### Rule: Content-Type Alert

Added the `Content-Type` as an alert rule. Results of the rule executing on a log file:

<img width="1044" height="487" alt="image" src="https://github.com/user-attachments/assets/f81a673d-5ac5-4acc-a8b9-7dd7df90ecbd" />

### Rule: Magic Bytes Detection (4D5A)

Additionally, a rule was created to look at the magic bytes of the file using the hexadecimal pattern `4D5A`.

- This is specific to this case, where the `MZ` signature was present in the malicious `.exe` file.
- The hex value was found on Wikipedia in a list of file signatures.

**Rule creation:**

<img width="1439" height="28" alt="image" src="https://github.com/user-attachments/assets/62832c8b-3ad3-473c-be9e-9589104cf733" />

**Packet captured and log file created:**

<img width="1493" height="56" alt="image" src="https://github.com/user-attachments/assets/54e81e7b-9355-4cfb-9f95-f3860cc7108b" />

**Log file in Wireshark with the MZ bytes present in the file:**

<img width="1218" height="498" alt="image" src="https://github.com/user-attachments/assets/4dcfe7af-6ae4-4e75-b74b-fbed50e40401" />

### Example 2: Unique User Agent (Cobalt Strike / SSLoad)

Using a pcap file analysed earlier, containing Cobalt Strike activity with a malicious SSLoad DLL that used a unique user agent string.

<img width="940" height="600" alt="image" src="https://github.com/user-attachments/assets/a82d8c24-5be3-4dcc-952c-d3dfff74d0f0" />

### After rule creation:

<img width="1317" height="183" alt="image" src="https://github.com/user-attachments/assets/a817a7ab-3ba3-4ef0-8df2-8eae2357e0cf" />

Both show 9 packets, meaning the rule successfully detected and alerted on all packets containing the user agent via the headers.

### Example 3: SSH Brute Force

A pcap packet capture containing an SSH brute force attack.

<img width="1108" height="107" alt="image" src="https://github.com/user-attachments/assets/201acbbe-732d-4017-9ba2-4840ebe671ca" />

The capture file properties show that all activity occurred within 25 seconds.

<img width="748" height="277" alt="image" src="https://github.com/user-attachments/assets/8154b0af-6bab-4cd8-9ce0-0fe1b5275fbf" />

**Goal:** Create a rule that tracks an IP address with more than 5 SSH attempts within 30 seconds.

**Results:**

The threshold was set to `both`, minimising the number of duplicates. If an endpoint attempts more than 5 SSH connections to an established TCP server, one alert is created instead of sending each attempt as a separate alert.

<img width="2356" height="42" alt="image" src="https://github.com/user-attachments/assets/95f8d514-3a3c-4306-ae77-5f700fffbb6d" />

### Challenge: LFI Exploitation and Brute Force:

**Scenario:** An attacker exploited LFI, and DLP alerts were triggered around the same timeframe, suggesting the attacker exfiltrated sensitive files from the server.

#### Brute Force Tool Identification:

The attacker used `Mozilla/4.0 (Hydra)` as their brute force tool to access the web server.

<img width="788" height="515" alt="image" src="https://github.com/user-attachments/assets/179c459c-9372-4f0c-ae8b-001941e94327" />

#### Rule: Failed Login Attempts:

The web server responds with `401` error codes for failed login attempts. Created a rule to detect 10 failed login attempts occurring within a 30-second period from the same IP address.

**Rule results:**

<img width="765" height="228" alt="image" src="https://github.com/user-attachments/assets/2d1a4677-a1bc-4936-9aef-475be8f3a46b" />

Out of the 20,987 packets, 174 were alerts.

#### Rule: Successful Logins:

Created a rule to check for any successful logins.

**Results of the rule:**

<img width="712" height="131" alt="image" src="https://github.com/user-attachments/assets/b14f7620-13f9-4248-a2fe-47b2888ed70a" />

**Timestamp:**

<img width="1165" height="127" alt="image" src="https://github.com/user-attachments/assets/641c49f9-6490-4be0-8b1d-c4dde8392703" />

#### Rule: LFI Bypass Technique (`../`)

Created a rule to check for the common LFI bypass technique, which is along the lines of `../`.

**Rule results:**

<img width="712" height="131" alt="image" src="https://github.com/user-attachments/assets/399f86d4-833d-44e4-8463-891e805a55fb" />

Note that obfuscation is a common bypass method, so recursion is recommended within filters and other protection methods.

#### Rule: Private SSH Key File Signatures:

Created a rule to check for file signatures of any private SSH keys.

**Results:**

<img width="425" height="118" alt="image" src="https://github.com/user-attachments/assets/01ead6ac-5529-4f45-a219-f68110655851" />

#### Attacker Information:

Attacker information based on the SSH connection IP address:

<img width="726" height="460" alt="image" src="https://github.com/user-attachments/assets/c25d411c-cd2d-4b02-9a9a-70f5c0567edd" />
