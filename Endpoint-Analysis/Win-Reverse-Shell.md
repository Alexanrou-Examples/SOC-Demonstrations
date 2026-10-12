# Reverse Shell

## Metasploit Payload Setup

Created the Metasploit payload and file. File creation itself is not shown, only setting up Metasploit is shown.

<img width="730" height="286" alt="image" src="https://github.com/user-attachments/assets/16e2e81d-3960-4ed1-b291-b170ed8f8bd0" />

## Python Server

Python server to connect to from the Windows machine (note that both VMs are configured on the same NAT network).

<img width="686" height="273" alt="image" src="https://github.com/user-attachments/assets/05178790-2ec1-4ce8-998c-c8cb2bc5b0bc" />

## Downloading the Malware

Visited the server from Windows and downloaded the malware.

<img width="860" height="360" alt="image" src="https://github.com/user-attachments/assets/e455b491-f3cc-494e-8579-4533d1622072" />

## Executing the Malware

Executed the malware on the Windows machine.

<img width="860" height="360" alt="image" src="https://github.com/user-attachments/assets/c519f646-caab-4ef7-a5b3-c0143adb41ce" />

As seen in the Python server screenshot, the reverse shell was successful.

## Shared File Access

The shared file where the attacker can access the information that is retrieved.

<img width="705" height="186" alt="image" src="https://github.com/user-attachments/assets/1c9b0334-335e-4f31-9296-1e9f9bcb89a9" />

## Lateral Movement Check

Can also view the resource section of `net share` to see if there is any lateral movement, etc.

<img width="509" height="164" alt="image" src="https://github.com/user-attachments/assets/d8852295-8786-40e3-8d95-9540cc58db4b" />

## View from the Windows Machine

This is one of the active network sessions, and as seen, the Meterpreter commands from the simulated attacker (me) are successful, as this was created from the Ubuntu machine shell.

<img width="642" height="121" alt="image" src="https://github.com/user-attachments/assets/84bff54f-02aa-4a56-b6aa-a369a0c8ddca" />
## Link Established

The link is established: 10.0.2.5 is the Ubuntu machine and .20 is Windows, shown by two different tools.

<img width="618" height="41" alt="image" src="https://github.com/user-attachments/assets/f4827b3c-af61-4548-ad90-c6d881551716" />


<img width="1182" height="535" alt="image" src="https://github.com/user-attachments/assets/5d17771c-0630-4671-9485-1e23c2143813" />

## Further Analysis with Native Windows Tools

<img width="632" height="97" alt="image" src="https://github.com/user-attachments/assets/86c4c367-01b0-4032-959e-e70d1f2b0cd4" />

### DLL Files

<img width="636" height="104" alt="image" src="https://github.com/user-attachments/assets/3c6f0283-efdc-4271-8d08-001f2a360390" />
