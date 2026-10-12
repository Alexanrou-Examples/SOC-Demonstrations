# Email Attachment Analysis

## Overview

This document details the process of extracting and analyzing a suspicious email
attachment, including hash generation, sandbox/tool analysis, VirusTotal lookups,
and infrastructure relationship mapping.

<img width="1102" height="777" alt="Screenshot From 2026-09-07 12-12-44" src="https://github.com/user-attachments/assets/11e71fe2-c90f-4555-8c85-3ec8ccaa9962" />


---

## 1. Attachment Extraction

Three possible extraction methods were considered:

| Method | Tool | Risk Level | Notes |
|--------|------|------------|-------|
| 1 | Save As | 🔴 High | Highly susceptible to user error (e.g. accidentally opening or executing the file) |
| 2 | `emldump.py` | 🟡 Medium | Extracts the attachment without the email client's GUI, but still saves the raw attachment to disk |
| 3 | `eioc.py` | 🟢 Low | **Recommended.** Safest option — only requires the path to the email file itself, no direct download or extraction |

---

## 2. File Analysis

### Hashes

<img width="877" height="123" alt="Screenshot From 2026-09-07 12-24-37" src="https://github.com/user-attachments/assets/b8294ca3-2694-4718-b418-c5c3e4a7190d" />


### `eioc.py` Output

<img width="954" height="480" alt="Screenshot From 2026-09-07 12-39-17" src="https://github.com/user-attachments/assets/d39d15da-8585-4760-a3c1-0679f0b0f9bf" />


### Windows PowerShell

<img width="1887" height="182" alt="Screenshot From 2026-09-07 12-51-52" src="https://github.com/user-attachments/assets/9513b851-b6e4-4708-aa02-6dead4311b1f" />


---

## 3. VirusTotal Results

The file hash was used for the VirusTotal lookup rather than uploading the file
itself. This is the safer approach in case the document contains sensitive
information.

<img width="1656" height="892" alt="Screenshot From 2026-09-07 12-54-12" src="https://github.com/user-attachments/assets/dadb4cae-8adc-4746-9d0c-dc654018abbd" />


### File Details

<img width="1200" height="805" alt="Screenshot From 2026-09-07 12-56-03" src="https://github.com/user-attachments/assets/ef0a0f16-fd83-4437-bec0-1709e05d1af9" />


> **Note:** The additional names listed for the file are useful for building
> detection filters and identifying related events before they escalate into
> incidents — or potentially preventing the incident from occurring altogether.

---

## 4. Relations

<img width="1195" height="761" alt="Screenshot From 2026-09-07 12-59-04" src="https://github.com/user-attachments/assets/54aa0f02-7769-44b6-9931-71d4af873f7e" />


The **Relations** tab reveals the domains and IP addresses involved in the
attachment's execution and communication process.

<img width="1488" height="626" alt="Screenshot From 2026-09-07 13-03-54" src="https://github.com/user-attachments/assets/86c6d0b3-f7d2-49ec-b6a8-0a07b18b074d" />


Notably, it also references a **root certificate from `apple.com`**. The reason
for this is not entirely clear — it may be an attempt to bypass certain filters
or lend the file an appearance of legitimacy (obfuscation).

---

## 5. Talos Results

<img width="1154" height="612" alt="Screenshot From 2026-09-07 13-06-29" src="https://github.com/user-attachments/assets/d979333a-b33d-42d7-8b6b-36cdf0fb5abf" />


---

## 6. Verdict

**Multiple analysis tools independently confirmed the file as malicious.**
