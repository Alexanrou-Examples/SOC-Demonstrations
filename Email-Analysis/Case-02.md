# Malware Analysis

## Hybrid Analysis

Used [Hybrid Analysis](https://www.hybrid-analysis.com/) to analyze a malicious spreadsheet.

<img width="1662" height="891" alt="Screenshot From 2026-09-08 09-56-35" src="https://github.com/user-attachments/assets/0dd225ce-278f-444b-a117-801ee578e245" />


This allowed me to observe how the malware behaves across different operating systems — in this case, Windows 11 vs. Windows 10.

> **Note:** Hybrid Analysis submissions are public by default, meaning the community can view whatever is analyzed. Do not submit files containing sensitive information.

The analysis surfaced contacted hosts, along with information such as their geolocation, as well as the fact that `powershell.exe` was present in the associated process tree.

<img width="1305" height="335" alt="Screenshot From 2026-09-08 10-04-15" src="https://github.com/user-attachments/assets/e854d0b1-82fb-4db3-aece-89f4e1135187" />



The attack chain used:

<img width="558" height="84" alt="Screenshot From 2026-09-08 10-14-16" src="https://github.com/user-attachments/assets/859181de-cbef-4db1-8b38-f4976406b9ce" />


The analysis detected that the spreadsheet executes PowerShell, which is not expected/legitimate behavior for a spreadsheet file.

<img width="558" height="84" alt="Screenshot From 2026-09-08 10-15-48" src="https://github.com/user-attachments/assets/4813e5f1-a3b5-456c-b12e-fc6559be02b0" />


## Joe Sandbox

- The free tier is limited, but it still allows configuration of certain sandbox aspects, such as network access, and displays basic analysis information.
- **Note:** Also a public platform, but offers a private, paid option.
- Joe Sandbox is interactive, allowing deeper investigation by manually testing the Excel file within the sandbox environment.

## Any.Run

- Broadly similar to Joe Sandbox — also limited on the free tier, but yields comparable results.
- If an analysis already exists for a given sample, you can view someone else's prior analysis, even on the free plan.
- Allows configuration of several sandbox parameters, including the starting object, target OS, and network configuration.
