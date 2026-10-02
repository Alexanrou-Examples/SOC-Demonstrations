# Phishing Email Analysis

## What This Is
A collection of detailed phishing email analyses demonstrating practical security investigation skills.

## How to Use
1. Browse the `CASE-XX/` folders for individual analyses
2. Each case includes step-by-step documentation with screenshots
3. Network analysis has `Wireshark/` cases, these are specific to the tool.

## Skills Demonstrated
- Email header analysis (SPF, DKIM, DMARC)
- URL extraction and deobfuscation
- Attachment forensics (hashing, reputation checks)
- Social engineering pattern recognition
- Threat intelligence integration

## Tools
CyberChef, VirusTotal, urlscan.io, MXToolbox, emldump.py
- Header Analysis
  - CyberChef, MHA, MXToolbox, Sublime Email Header Plugin
- Hashing
   - sha256sum, sha1sum, md5sum, PowerShell Get-FileHash
- Reputation
   - VirusTotal, Talos, PhishTank, URLVoid, URLhaus
- URL Analysis
   - urlscan.io, unshorten.it, dnstwist, Google Safe Browsing
- Forensics
   - emldump.py, Email-IOC-Extractor, Cybershelf
- Documentation
  - Screenshot capture, CLI logging, Markdown reporting

## Security Best Practices Demonstrated
- Defanging: Modifying hyperlinks to prevent accidental clicks
- Safe Inspection: Using sandboxed tools (Wannabrowser, URL2PNG) instead of direct navigation
- Privacy Awareness: Avoiding sensitive data submission to public VirusTotal
- Audit Trail Maintenance: Complete documentation for incident justification
- Cross-Validation: Multiple tool correlation before verdicts
