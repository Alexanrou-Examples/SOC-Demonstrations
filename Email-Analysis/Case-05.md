# Phishing Analysis Report — Challenge 1

## Headers

| Field | Value |
|---|---|
| Date | 2023/10/31, 19:10 |
| Subject | Your account has been flagged for unusual activity |
| To | dderringer@mighty-solutions.net |
| From | Outlook Support Team \<social201511138@social.helwan.edu.eg\> |
| Reply-To | — |
| Return-Path | social201511138@social.helwan.edu.eg |
| Bounced Email | social201511138@social.helwan.edu.eg |
| Sender IP | 40.107.22.60 |
| Resolved Host | mail-am6eur05on2060.outbound.protection.outlook.com |
| Sender IP Owner | Microsoft Corporation |
| Message-ID | JMrByPl2c3HBo8SctKnJ5C5Gp64sPSSWk76p4sjQ@s6 |

## URLs

```
hxxps[://]raw[.]githubusercontent[.]com/MalwareCube/SOC101/main/assets/01_Phishing_Analysis/microsoft[.]jpg
hxxps[://]0[.]232[.]205[.]92[.]host[.]secureserver[.]net/lclbluewin08812/
```

## Attachments

| Field | Value |
|---|---|
| Attachment Name | — |
| MD5 | — |
| SHA1 | — |
| SHA256 | — |

## Description

A high-ranking employee received a suspicious email containing multiple URLs, a sense of urgency, and a spoofed sender domain.

## Authentication Checks

| Check | Result |
|---|---|
| SPF | Pass |
| DMARC | Best guess pass |
| DKIM | Pass |

All three checks pass because the email genuinely originates from Microsoft's outbound mail infrastructure (`protection.outlook.com`). This does not indicate legitimacy — the phishing element is a compromised or attacker-registered mailbox on an unrelated domain (`social.helwan.edu.eg`) sending under a spoofed "Outlook Support Team" display name, not a spoofed envelope.

## Artifact Analysis

**Sender Analysis:** The From address (`social201511138@social.helwan.edu.eg`) belongs to an unrelated domain and has no legitimate connection to Microsoft. The display name "Outlook Support Team" is used to disguise this mismatch from the recipient. Return-Path and bounce address match the sending address, consistent with a compromised or attacker-controlled mailbox rather than a spoofed header.

**URL Analysis:** The first URL hosts an image, likely used to visually impersonate Microsoft branding in the email body. The second URL resolves to a redirect to a image/png likely the method used by the attacker to achieve their goal.

**Attachment Analysis:** No attachments present.

## Verdict

Phishing attack.

## Defense Actions

- Block the sender IP via an EDR rule and a mail filter rule.
- Report the abuse to Microsoft via their abuse submission page, providing the required information.

## Screenshots

**Reverse DNS lookup**

<img width="742" height="716" alt="Screenshot From 2026-09-10 09-34-04" src="https://github.com/user-attachments/assets/614063af-782c-4399-ba6b-5bc0c7c1094f" />



**CyberChef encoding**

<img width="1521" height="816" alt="Screenshot From 2026-09-10 09-52-35" src="https://github.com/user-attachments/assets/9a32374d-cefd-45c7-a917-326c9fabb47d" />



**Extracted and defanged information**

<img width="888" height="531" alt="Screenshot From 2026-09-10 09-52-58" src="https://github.com/user-attachments/assets/35a743c5-4ca6-4a33-bc70-db09abb80bca" />



**SPF record**

<img width="883" height="141" alt="Screenshot From 2026-09-10 10-00-06" src="https://github.com/user-attachments/assets/6d3481e0-51c0-4fb1-81f2-a9d63155776a" />



**VirusTotal result on URL**

<img width="1661" height="878" alt="Screenshot From 2026-09-10 09-55-38" src="https://github.com/user-attachments/assets/0d0cc8ce-e964-4ce9-b50b-cf4cde15890a" />
