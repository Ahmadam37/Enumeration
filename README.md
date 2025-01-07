# Enumeration


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

