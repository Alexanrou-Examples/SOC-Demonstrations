# Reverse Shell

## Metasploit Payload Setup

Created the Metasploit payload and file. File creation itself is not shown, only setting up Metasploit is shown.

<img width="730" height="286" alt="image" src="https://github.com/user-attachments/assets/095e46aa-b582-4145-a0b5-e47ff686eb64" />

## Python Server

Python server to connect to from the Windows machine (note that both VMs are configured on the same NAT network).

<img width="686" height="273" alt="image" src="https://github.com/user-attachments/assets/dc9e999f-7479-47af-96f8-f8c477a6df9b" />

## Downloading the Malware

Visited the server from Windows and downloaded the malware.

<img width="860" height="360" alt="image" src="https://github.com/user-attachments/assets/dfe73f96-430b-49e6-bfeb-3687e2fee985" />

## Executing the Malware

Executed the malware on the Windows machine.

<img width="860" height="360" alt="image" src="https://github.com/user-attachments/assets/f1bd918f-85a0-49dc-b003-5d7643ee28b1" />

As seen in the Python server screenshot, the reverse shell was successful.

## Shared File Access

The shared file where the attacker can access the information that is retrieved.

<img width="705" height="186" alt="image" src="https://github.com/user-attachments/assets/9a907ab1-d813-405e-92d8-5f57cabd5f7e" />

## Lateral Movement Check

Can also view the resource section of `net share` to see if there is any lateral movement, etc.

<img width="509" height="164" alt="image" src="https://github.com/user-attachments/assets/fd1ee744-526f-4ace-a61b-6086f654b8b2" />

## View from the Windows Machine

This is one of the active network sessions, and as seen, the Meterpreter commands from the simulated attacker (me) are successful, as this was created from the Ubuntu machine shell.

<img width="642" height="121" alt="image" src="https://github.com/user-attachments/assets/6aea1a9a-6cbf-4c46-b637-4a19aedea82b" />

## Link Established

The link is established: 10.0.2.5 is the Ubuntu machine and .20 is Windows, shown by two different tools.

<img width="618" height="41" alt="image" src="https://github.com/user-attachments/assets/023cc218-4d5c-4dab-84cb-ee5537d2eeb5" />


<img width="1182" height="535" alt="image" src="https://github.com/user-attachments/assets/e835ae1e-6dd3-4f15-820c-9159a7d97f16" />

## Further Analysis with Native Windows Tools

<img width="632" height="97" alt="image" src="https://github.com/user-attachments/assets/2d3759b2-d3b8-413c-9ae3-650d95623db5" />

### DLL Files

<img width="636" height="104" alt="image" src="https://github.com/user-attachments/assets/2e360e22-b767-4263-a1f5-839cd187a41c" />
