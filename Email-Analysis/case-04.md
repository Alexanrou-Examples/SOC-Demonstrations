# Automated Email Analysis

This case study revisits the same email analyzed manually in a previous write-up, this time using automated tooling for comparison.

<img width="1589" height="675" alt="Screenshot From 2026-09-09 09-28-02" src="https://github.com/user-attachments/assets/1d155461-b91e-4b41-87d8-ea4ac97871e3" />


## PhishTool Results

PhishTool flagged the following indicators, which align with my manual findings but were produced far more efficiently.

<img width="743" height="299" alt="Screenshot From 2026-09-09 09-30-14" src="https://github.com/user-attachments/assets/f773828b-d788-4926-b42e-8907fb851ed5" />


<img width="742" height="396" alt="Screenshot From 2026-09-09 09-32-12" src="https://github.com/user-attachments/assets/b3a243f0-7863-41cf-9204-6cb30853fd2e" />


## Resolved DNS

The tool also returned resolved DNS information, which is very convenient compared to manual testing.

<img width="420" height="65" alt="Screenshot From 2026-09-09 09-32-55" src="https://github.com/user-attachments/assets/2f94322c-1fa7-479d-bec0-6c028caca405" />


> **Note:** This doesn't make manual testing obsolete. Automated tools are convenient, but they can miss indicators depending on the angle an attacker takes when targeting a victim. An analyst should still know what to look for and be able to recognize when further manual analysis of a given object is warranted.

## Integrations

PhishTool supports integration with other tools, such as VirusTotal, via an API key.
