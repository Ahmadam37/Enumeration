# Service Enumeration



# Passive Enumeration

Passive Enumeration is gathering information publicly on the internet. Passive enumeration involves interacting with the target system to gather this information.

## Step 1: Analyze DNS and Website Technology

Start by examining the DNS and the technology of the website. Use the following commands in the command line:

```bash
whatis host website.com
host
whois website.com
dnsrecon -d website.com
wafw00f www.website.com
sublist3r -d www.website.com  # If sublist3r doesn’t work, try using a VPN and try again
````
If sublist3r doesn't work, you can use Google Dorks or theHarvester to enumerate subdomains.

Google Dorks:

1. site:website.com
2. site:website inurl:admin  # Search for directories like admin, forum, blog, etc.
3. site:*.website.com  # Enumerate all subdomains like sublist3r
4. site:*.website.com intitle:admin
5. site:*.website.com filetype:pdf OR filetype:xml OR filetype:docx
6. intitle:index of
7. site:gov.* intitle:"index of" *.csv
8. site:gov.* intitle:"index of" *.csv passwords


You can visit the Google Hacking Database for more dork examples.

nslookup Tool:
To gather DNS-related information, use nslookup:

nslookup example.com
nslookup -query=mx example.com  # Get MX record
nslookup -type=ns example.com  # Get nameserver record


You can also enumerate subdomains using:

theHarvester -d website.com -b google,linkedin
# If no results, try:
theHarvester -d website.com -b all

If you find emails, you can check them at Have I Been Pwned to see if any leaked passwords exist. https://haveibeenpwned.com/



Certainly! Here’s the full content you provided, formatted with GitHub markdown:

markdown
Copy code
# Passive Enumeration

Passive Enumeration is gathering information publicly on the internet. Passive enumeration involves interacting with the target system to gather this information.

## Step 1: Analyze DNS and Website Technology

Start by examining the DNS and the technology of the website. Use the following commands in the command line:

```bash
whatis host website.com
host
whois website.com
dnsrecon -d website.com
wafw00f www.website.com
sublist3r -d www.website.com  # If sublist3r doesn’t work, try using a VPN and try again
If sublist3r doesn't work, you can use Google Dorks or theHarvester to enumerate subdomains.
```
Google Dorks:
text
Copy code
1. site:website.com
2. site:website inurl:admin  # Search for directories like admin, forum, blog, etc.
3. site:*.website.com  # Enumerate all subdomains like sublist3r
4. site:*.website.com intitle:admin
5. site:*.website.com filetype:pdf OR filetype:xml OR filetype:docx
6. intitle:index of
7. site:gov.* intitle:"index of" *.csv
8. site:gov.* intitle:"index of" *.csv passwords
You can visit the Google Hacking Database for more dork examples.

nslookup Tool:
To gather DNS-related information, use nslookup:

bash
Copy code
nslookup example.com
nslookup -query=mx example.com  # Get MX record
nslookup -type=ns example.com  # Get nameserver record
You can also enumerate subdomains using:

bash
Copy code
theHarvester -d website.com -b google,linkedin
# If no results, try:
theHarvester -d website.com -b all
If you find emails, you can check them at Have I Been Pwned to see if any leaked passwords exist.

Active Enumeration
Active Enumeration involves interacting directly with the target system. This method can trigger logs, alerts, or intrusion detection systems (IDS), so caution is necessary.

Step 1: Using dnsenum Tool
To find all subdomains, use dnsenum:
```bash
dnsenum website.com
```
You can also use dig for DNS lookups:

```bash
dig axfr @nsRecord website.com  # Zone transfer

```

Alternatively, you can use the fierce tool:

```bash

fierce --domain website.com

```

Step 2: Nmap Tool
Nmap (Network Mapper) is a powerful tool for network exploration and security auditing.

Common Nmap Commands:

```bash
1. sudo nmap -sn ip/website.com  # Ping scan
2. nmap -Pn IP  # Disable host discovery
3. nmap -Pn -p 80  # Scan specific port
4. sudo nmap -Pn -F 172.104.174.50 -v  # Fast scan with verbose output
5. nmap -Pn -F -sV ip  # Fast scan with service version detection
6. sudo nmap -Pn -F -sV -O 172.104.174.50  # OS detection
7. sudo nmap -Pn -sC 172.104.174.50 -v  # Run script scan
8. sudo nmap -Pn -sU 172.104.174.50  # UDP port scan

```
For output in text format:

```bash
nmap -Pn -F ip -oN text.txt
cat text.txt

```

For XML output:

```bash
nmap -Pn -F ip -oX text.xml
cat text.xml
```

Netdiscover Tool
Netdiscover is another tool for discovering devices on a network:
```bash
sudo netdiscover -i network -r ip
```

Exploit the Process
Once you have performed a port scan and service identification, you can proceed to exploit identified services.

Commands to Discover Hosts:

```bash
1. ping -c 4 ip  # Check if the IP responds
2. nmap ip  # Scan the target
3. nmap -p- ip  # Scan all ports
4. nmap -pPORT1,PORT2,PORT3 -sV ip  # Scan specific ports
```

Discover Hosts Behind Firewalls:

```bash
1. ping -c 4 ip
2. nmap ip
3. nmap -Pn ip  # Disable host discovery
4. nmap -Pn -pPORT ip  # Scan specific port, firewall might filter
5. nmap -Pn -sV -p 80 ip  # Scan HTTP service
```

Capture The Flag (CTF)
Flag 1: FTP Access
In the CTF challenge, you can use FTP to access a target:

```bash
ftp ip
username: Anonymous
password: gust@gmail.com
ls  # List files
get [fileName]  # Download file
```
Flag 2: robots.txt
You can find the target's robots.txt by navigating to:

```bash
example.com/robots.txt
```

You can also check specific files listed there, for example:
```text
example.com/theFileName
```


Flag 3: MySQL
To access the MySQL database, use:

```bash
mysql -h ip -u username -p  # Login to MySQL
```

Once logged in, you can list databases with:


```bash
show databases;
```

Auxiliary Modules in Metasploit
Auxiliary modules are used for scanning, discovery, and fuzzing. These modules can also be used post-exploitation within an internal network.

Questions about Metasploit's Auxiliary Modules:
What is an auxiliary module in the Metasploit framework primarily used for?

Scanning and network discovery.
When setting up a port scan using Metasploit auxiliary modules, what is an important option you often need to configure?

Hosts and port range.
What might you choose to use an auxiliary module for port scanning during a pentest if you already have Nmap results?

Use an auxiliary module during the post-exploitation phase.
To search for specific modules in Metasploit:

```bash
msf5> search type: auxiliary name:ftp
```
Then use the desired module:

```bash
msf5> use auxiliary/scanner/ftp/ftp_login
```

Summary of Steps:
To explore multiple targets, you need to first scan the first target to gain permission to proceed with the second target. Steps include:

```bash
1. ping -c 5 ip
2. nmap ip  # Get the target IP address
```




# FTP Enumeration:

The ftp are using 21 port by defualt, but it can be using any port

This is a very simple way to test the FTP port.
```bash
nmap -p 21 ip 
```
If the port 21 closed you can try to test all port on the target IP.

```bash
nmap -p- IP
```
Sometimes FTP services run on common alternate ports like 5554,2121, 8021, or others.

- Try to log-in throgh FTP 

ftp IP PORT
```bash
ftp 193.9.0.2 5554
```

## FTP Script Scanning 

you have to search for FTP 

```bash
ls -al /usr/share/nmap/scripts/ | grep -e "ftp"
```

After this command you will see all FTP options.

```bash
-rw-r--r-- 1 root root  4530 Jun 20  2024 ftp-anon.nse
-rw-r--r-- 1 root root  3253 Jun 20  2024 ftp-bounce.nse
-rw-r--r-- 1 root root  3108 Jun 20  2024 ftp-brute.nse
-rw-r--r-- 1 root root  3272 Jun 20  2024 ftp-libopie.nse
-rw-r--r-- 1 root root  3290 Jun 20  2024 ftp-proftpd-backdoor.nse
-rw-r--r-- 1 root root  3768 Jun 20  2024 ftp-syst.nse
-rw-r--r-- 1 root root  6021 Jun 20  2024 ftp-vsftpd-backdoor.nse
-rw-r--r-- 1 root root  5923 Jun 20  2024 ftp-vuln-cve2010-4221.nse
-rw-r--r-- 1 root root  5736 Jun 20  2024 tftp-enum.nse
-rw-r--r-- 1 root root 10034 Jun 20  2024 tftp-version.nse
  
```
Then you can specifie the option you want.

```bash
nmap -sV --script=tftp-version.nse IP
```

The result 
```bash
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-07 16:16 IST
Nmap scan report for example.com (IP)
Host is up (0.000012s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     ProFTPD 1.3.5a
MAC Address: 02:42:C0:65:46:03 (Unknown)
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.29 seconds
```

Also you can use Metasploit for FTP enumeration.

IF you want to use Metasploit you have to start the database.

```bash
service postgresql start
```
Then start Metasploit Framework.

```bash
msfconsole
```

After that you can use Metasploit
```bash
┌──(root)-[~]
└─# msfconsole                                                                                                                                             
Metasploit tip: Save the current environment with the save command, 
future console restarts will use this environment again
                                                  

  Metasploit Park, System Security Interface                                                                                                               
  Version 4.0.5, Alpha E                                                                                                                                   
  Ready...                                                                                                                                                 
  > access security                                                                                                                                        
  access: PERMISSION DENIED.
  > access security grid
  access: PERMISSION DENIED.
  > access main security grid
  access: PERMISSION DENIED....and...
  YOU DIDN'T SAY THE MAGIC WORD!
  YOU DIDN'T SAY THE MAGIC WORD!                                                                                                                           
  YOU DIDN'T SAY THE MAGIC WORD!                                                                                                                           
  YOU DIDN'T SAY THE MAGIC WORD!                                                                                                                           
  YOU DIDN'T SAY THE MAGIC WORD!                                                                                                                           
  YOU DIDN'T SAY THE MAGIC WORD!                                                                                                                           
  YOU DIDN'T SAY THE MAGIC WORD!                                                                                                                           


       =[ metasploit v6.4.12-dev                          ]
+ -- --=[ 2426 exploits - 1250 auxiliary - 428 post       ]
+ -- --=[ 1468 payloads - 47 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

msf6 > 
```
Here how you search in Metasploit for FTP.
```bash
msf6 > search type:auxiliary name:ftp
```
This is the result.
```bash
msf6 > search type:auxiliary name:ftp

Matching Modules
================

   #   Name                                                  Disclosure Date  Rank    Check  Description
   -   ----                                                  ---------------  ----    -----  -----------
   0   auxiliary/scanner/ftp/anonymous                       .                normal  No     Anonymous FTP Access Detection
   1   auxiliary/server/capture/ftp                          .                normal  No     Authentication Capture: FTP
   2   auxiliary/scanner/ftp/bison_ftp_traversal             2015-09-28       normal  Yes    BisonWare BisonFTP Server 3.5 Directory Traversal Information Disclosure
   3   auxiliary/scanner/ssh/cerberus_sftp_enumusers         2014-05-27       normal  No     Cerberus FTP Server SFTP Username Enumeration
   4   auxiliary/scanner/snmp/cisco_config_tftp              .                normal  No     Cisco IOS SNMP Configuration Grabber (TFTP)
   5   auxiliary/scanner/snmp/cisco_upload_file              .                normal  No     Cisco IOS SNMP File Upload (TFTP)
   6     \_ action: Override_Config                          .                .       .      Override the running config
   7     \_ action: Upload_File                              .                .       .      Upload the file
   8   auxiliary/admin/networking/cisco_vpn_3000_ftp_bypass  2006-08-23       normal  No     Cisco VPN Concentrator 3000 FTP Unauthorized Administrative Access
   9   auxiliary/scanner/ftp/colorado_ftp_traversal          2016-08-11       normal  Yes    ColoradoFTP Server 1.3 Build 8 Directory Traversal Information Disclosure
   10  auxiliary/gather/crushftp_fileread_cve_2024_4040      .                normal  Yes    CrushFTP Unauthenticated Arbitrary File Read
   11  auxiliary/scanner/ftp/easy_file_sharing_ftp           2017-03-07       normal  Yes    Easy File Sharing FTP Server 3.6 Directory Traversal
   12  auxiliary/scanner/ftp/ftp_login                       .                normal  No     FTP Authentication Scanner
   13  auxiliary/scanner/portscan/ftpbounce                  .                normal  No     FTP Bounce Port Scanner
   14  auxiliary/server/ftp                                  .                normal  No     FTP File Server
   15  auxiliary/scanner/ftp/ftp_version                     .                normal  No     FTP Version Scanner
   16  auxiliary/dos/windows/ftp/filezilla_admin_user        2005-11-07       normal  No     FileZilla FTP Server Admin Interface Denial of Service
   17  auxiliary/dos/windows/ftp/filezilla_server_port       2006-12-11       normal  No     FileZilla FTP Server Malformed PORT Denial of Service
   18  auxiliary/server/wget_symlink_file_write              2014-10-27       normal  No     GNU Wget FTP Symlink Arbitrary Filesystem Access
   19  auxiliary/dos/scada/d20_tftp_overflow                 2012-01-19       normal  No     General Electric D20ME TFTP Server Buffer Overflow DoS
   20  auxiliary/dos/windows/ftp/guildftp_cwdlist            2008-10-12       normal  No     Guild FTPd 0.999.8.11/0.999.14 Heap Corruption
   21  auxiliary/scanner/tftp/ipswitch_whatsupgold_tftp      2011-12-12       normal  No     IpSwitch WhatsUp Gold TFTP Directory Traversal
   22  auxiliary/scanner/ftp/konica_ftp_traversal            2015-09-22       normal  Yes    Konica Minolta FTP Utility 1.00 Directory Traversal Information Disclosure
   23  auxiliary/dos/windows/ftp/iis75_ftpd_iac_bof          2010-12-21       normal  No     Microsoft IIS FTP Server Encoded Response Overflow Trigger
   24  auxiliary/dos/windows/ftp/iis_list_exhaustion         2009-09-03       normal  No     Microsoft IIS FTP Server LIST Stack Exhaustion
   25  auxiliary/scanner/tftp/netdecision_tftp               2009-05-16       normal  No     NetDecision 4.2 TFTP Directory Traversal
   26  auxiliary/scanner/ftp/pcman_ftp_traversal             2015-09-28       normal  Yes    PCMan FTP Server 2.0.7 Directory Traversal Information Disclosure
   27  auxiliary/dos/windows/tftp/pt360_write                2008-10-29       normal  No     PacketTrap TFTP Server 2.2.5459.0 DoS
   28  auxiliary/fuzzers/ftp/client_ftp                      .                normal  No     Simple FTP Client Fuzzer
   29  auxiliary/fuzzers/ftp/ftp_pre_post                    .                normal  No     Simple FTP Fuzzer
   30  auxiliary/dos/windows/ftp/solarftp_user               2011-02-22       normal  No     Solar FTP Server Malformed USER Denial of Service
   31  auxiliary/dos/windows/tftp/solarwinds                 2010-05-21       normal  No     SolarWinds TFTP Server 10.4.0.10 Denial of Service
   32  auxiliary/scanner/tftp/tftpbrute                      .                normal  No     TFTP Brute Forcer
   33  auxiliary/server/tftp                                 .                normal  No     TFTP File Server
   34  auxiliary/admin/tftp/tftp_transfer_util               .                normal  No     TFTP File Transfer Utility
   35    \_ action: Download                                 .                .       .      Download REMOTE_FILENAME as FILENAME from the server.
   36    \_ action: Upload                                   .                .       .      Upload FILENAME as REMOTE_FILENAME to the server.
   37  auxiliary/scanner/http/titan_ftp_admin_pwd            .                normal  No     Titan FTP Administrative Password Disclosure
   38  auxiliary/dos/windows/ftp/titan626_site               2008-10-14       normal  No     Titan FTP Server 6.26.630 SITE WHO DoS
   39  auxiliary/scanner/ftp/titanftp_xcrc_traversal         2010-06-15       normal  No     Titan FTP XCRC Directory Traversal Information Disclosure
   40  auxiliary/dos/ftp/vsftpd_232                          2011-02-03       normal  Yes    VSFTPD 2.3.2 Denial of Service
   41  auxiliary/dos/windows/ftp/vicftps50_list              2008-10-24       normal  No     Victory FTP Server 5.0 LIST DoS
   42  auxiliary/dos/windows/ftp/winftp230_nlst              2008-09-26       normal  No     WinFTP 2.3.0 NLST Denial of Service
   43  auxiliary/dos/windows/ftp/xmeasy560_nlst              2008-10-13       normal  No     XM Easy Personal FTP Server 5.6.0 NLST DoS
   44  auxiliary/dos/windows/ftp/xmeasy570_nlst              2009-03-27       normal  No     XM Easy Personal FTP Server 5.7.0 NLST DoS


Interact with a module by name or index. For example info 44, use 44 or use auxiliary/dos/windows/ftp/xmeasy570_nlst

```

Then you can choose any Thing of it by doing this.

```bash
msf6 > use auxiliary/scanner/ftp/ftp_version
```

```bash
msf6 auxiliary(scanner/ftp/ftp_version) > 
```

Then you can show options for the ftp_version

```bash
msf6 auxiliary(scanner/ftp/ftp_version) > show options
```
These all options in the ftp_version, and you have to set the RHOSTS to enumerate the version for the target IP 
```bash
msf6 auxiliary(scanner/ftp/ftp_version) > show options

Module options (auxiliary/scanner/ftp/ftp_version):

   Name     Current Setting      Required  Description
   ----     ---------------      --------  -----------
   FTPPASS  mozilla@example.com  no        The password for the specified username
   FTPUSER  anonymous            no        The username to authenticate as
   RHOSTS                        yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT    21                   yes       The target port (TCP)
   THREADS  1                    yes       The number of concurrent threads (max one per host)


View the full module info with the info, or info -d command.
```

How to set value for one of the options.
```bash
msf6 auxiliary(scanner/ftp/ftp_version) > set RHOSTS 1.1.1.1
RHOSTS => 1.1.1.1
```




# Lab Description:
This lab focuses on enumeration techniques to identify and analyze running services on a target Linux machine. The goal is to explore and interact with the machine's services to uncover and capture hidden flags. Participants will apply their knowledge of network and system enumeration to identify misconfigurations, weak credentials, and potential security vulnerabilities.

## Tasks

Lab Environment
A Linux machine is accessible at target.ine.local. Identify the services running on the machine and capture the flags. The flag is an md5 hash format.

Flag 1: There is a samba share that allows anonymous access. Wonder what's in there!
Flag 2: One of the samba users have a bad password. Their private share with the same name as their username is at risk!
Flag 3: Follow the hint given in the previous flag to uncover this one.
Flag 4: This is a warning meant to deter unauthorized users from logging in.

Note: The wordlists located in the following directory will be useful:

/root/Desktop/wordlists

Tools

Nmap
Metasploit
Hydra
enum4linux
smbclient
smbmap


Note
In this lab, the flag will follow the format: FLAG1{MD5Hash}. For example, FLAG1{0f4d0db3668dd58cabb9eb409657eaa8}. You need to submit only the MD5 hash string, excluding the braces. For instance: 0f4d0db3668dd58cabb9eb409657eaa8.





