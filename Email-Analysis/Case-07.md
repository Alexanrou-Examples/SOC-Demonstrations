# Phishing Analysis Report | Challenge 3

## Headers

| Field | Value |
|---|---|
| Date | 2024/05/14, 23:31 |
| Subject | You're Invited! |
| To | emily.nguyen@glbllogistics.co |
| From | Adam Barry \<abarry@live.com\> |
| Email Body | States "Alexia" instead of "Adam" |
| Reply-To | — |
| Return-Path | — |
| Sender IP | 2a01:111:f403:2c14::801 |
| Resolved Host | — |
| ASN | — |
| Message-ID | SA1PR14MB737384979FDD1178FD956584C1E32@SA1PR14MB7373.namprd14.prod.outlook.com |

## URLs

In-attachment redirect:

```
hxxps[://]github[.]com/TCWUS/Pastebin-Uploader[.]exe
```

## Attachments

| Field | Value |
|---|---|
| Filename | AR_Wedding_RSVP.docm |
| MD5 | 590d3c98cb5e61ea3e4226639d5623d7 |
| SHA1 | 91091f8e95909e0bc83852eec7cac4c04e1a57c3 |
| SHA256 | 41c3dd4e9f794d53c212398891931760de469321e4c5d04be719d5485ed8f53e |

## Description

Invitation from the employee's friend, with an attachment.

## Artifact Analysis

**Sender Analysis:** `abarry@live.com`. The name in the header is "Adam," but the name used in the email body is "Alexia" — a mismatch suggesting the sender identity is spoofed or reused from a different template/target.

**URL Analysis:** —

**Attachment Analysis:** The attachment contains a macro that redirects to a GitHub link:

```
hxxps[://]github[.]com/TCWUS/Pastebin-Uploader[.]exe
```

The macro also uses `shost.exe` in order to save the downloaded executable.

## Verdict

Malicious

## Defense Actions

- Block the IP by adding an EDR rule as well as a mail filter rule.
- Add the attachment to EDR rules (by hash).
- Check for related emails sent to other employees using one of the attacker's unique indicators (e.g. sender IP, attachment hash).

## Screenshots

<img width="970" height="135" alt="Screenshot From 2026-09-10 11-46-57" src="https://github.com/user-attachments/assets/33d7d3b0-9b6f-4886-a5be-a8765a8b12e4" />


<img width="1786" height="891" alt="Screenshot From 2026-09-10 11-47-48" src="https://github.com/user-attachments/assets/64683f4f-8b35-4e4c-a8c7-657e01e2acc2" />


<img width="361" height="50" alt="Screenshot From 2026-09-10 11-51-13" src="https://github.com/user-attachments/assets/7dd3263c-540e-4dca-a372-600ae5a03b2f" />


<img width="1129" height="268" alt="Screenshot From 2026-09-10 12-00-13" src="https://github.com/user-attachments/assets/ad7bdfcf-4078-4c93-b0d6-e68b6f8f8311" />


<img width="1553" height="843" alt="Screenshot From 2026-09-10 11-42-06" src="https://github.com/user-attachments/assets/1a494ad6-0bd0-4e02-8e11-0c24738faf2f" />
