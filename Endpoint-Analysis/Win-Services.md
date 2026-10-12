Windows Services Case Study

Same malware and reverse shell as in the other case studies, but focused on Windows services.

Attacker Machine (Ubuntu Reverse Shell)

<img width="1107" height="49" alt="image" src="https://github.com/user-attachments/assets/9e019176-ee7d-40dc-96fc-7ef03b3d8d8e" />

<img width="1107" height="49" alt="image" src="https://github.com/user-attachments/assets/4cf25b0f-e1e5-4513-a298-a7f5c65e9e70" />

The service is set to auto-start, so every time the Windows machine restarts, the "BackupService" will start automatically and execute the reverse shell.
Windows Services GUI

Viewing the service with the native Windows Services application:

<img width="986" height="426" alt="image" src="https://github.com/user-attachments/assets/82e64bbc-ad40-4cf8-8d0e-0c11009563b0" />

<img width="409" height="461" alt="image" src="https://github.com/user-attachments/assets/a6cdc9e4-24e0-4d4b-8309-c0083464f36d" />

Command Prompt (CMD)

Viewing the service in CMD in case access to the GUI is not available.

Identification:

<img width="484" height="172" alt="image" src="https://github.com/user-attachments/assets/3d44c529-37a1-4b39-9f08-11d47af1b844" />

More info on the service:

<img width="665" height="258" alt="image" src="https://github.com/user-attachments/assets/bf878c8b-0453-4ade-aa92-5652d63ceba8" />

PowerShell

<img width="551" height="276" alt="image" src="https://github.com/user-attachments/assets/bf91b7f6-1857-4faa-98b4-97377c38aaa0" />


<img width="944" height="519" alt="image" src="https://github.com/user-attachments/assets/b5bb7c15-5143-4cd4-8540-bb47f0b7db55" />


<img width="944" height="519" alt="image" src="https://github.com/user-attachments/assets/d7fe0a4f-ef74-4016-8db7-0ec0d66ed9c7" />
