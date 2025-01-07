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






