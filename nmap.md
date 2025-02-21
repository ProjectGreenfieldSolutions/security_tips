# NMAP

## Determine OS based on response

### Code block
```
pentester$ sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace --disable-arp-ping

Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 00:12 CEST
SENT (0.0107s) ICMP [10.10.14.2 > 10.129.2.18 Echo request (type=8/code=0) id=13607 seq=0] IP [ttl=255 id=23541 iplen=28 ]
RCVD (0.0152s) ICMP [10.129.2.18 > 10.10.14.2 Echo reply (type=0/code=0) id=13607 seq=0] IP [ttl=128 id=40622 iplen=28 ]
Nmap scan report for 10.129.2.18
Host is up (0.086s latency).
MAC Address: DE:AD:00:00:BE:EF
Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds
```
### Helpful tips
- Windows typically are configured to have a time-to-live ("TTL") of 128
- Linux / Unix typically are configured to have a time-to-live ("TTL") of 64
- Cisco devices / network appliances often use a default configuration of time-to-live ("TTL") of 255

## Output for humans
### Tools
- **xsltproc** is a command line tool for applying XSLT stylesheets to XML documents. 

### Code block
```
pentester$ xsltproc target.xml -o target.html
```

### Output 
Results in a visually pleasant output of the nmap command

## Nmap Scripting Engine (NSE)

## Whats it for?
Allows creation of scripts to interact with targeted services, written in LUA

### Nmap Script Categories
| Category   | Description |
|------------|--------------------------------------------------------------------------------------------------------------------------------|
| **auth**   | Determination of authentication credentials. |
| **broadcast** | Scripts used for host discovery by broadcasting, where discovered hosts can be automatically added to scans. |
| **brute**  | Executes scripts that try to log in to the respective service by brute-forcing with credentials. |
| **default** | Default scripts executed by using the `-sC` option. |
| **discovery** | Evaluation of accessible services. |
| **dos** | These scripts check services for denial-of-service vulnerabilities but are used less as they can harm services. |
| **exploit** | Attempts to exploit known vulnerabilities for the scanned port. |
| **external** | Uses external services for further processing. |
| **fuzzer** | Identifies vulnerabilities and unexpected packet handling by sending different fields, which can take much time. |
| **intrusive** | Intrusive scripts that could negatively affect the target system. |
| **malware** | Checks if the target system is infected with malware. |
| **safe** | Defensive scripts that do not perform intrusive or destructive actions. |
| **version** | Extends service detection capabilities. |
| **vuln** | Identifies specific vulnerabilities. |

### Examples
```
pentester$ sudo nmap 10.129.2.28 -p 80 -sV --script vuln

map scan report for 10.129.2.28
Host is up (0.036s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
| http-enum:
|   /wp-login.php: Possible admin folder
|   /readme.html: Wordpress version: 2
|   /: WordPress version: 5.3.4
|   /wp-includes/images/rss.png: Wordpress version 2.2 found.
|   /wp-includes/js/jquery/suggest.js: Wordpress version 2.5 found.
|   /wp-includes/images/blank.gif: Wordpress version 2.6 found.
|   /wp-includes/js/comment-reply.js: Wordpress version 2.7 found.
|   /wp-login.php: Wordpress login page.
|   /wp-admin/upgrade.php: Wordpress login page.
|_  /readme.html: Interesting, a readme.
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
| http-wordpress-users:
| Username found: admin
|_Search stopped at ID #25. Increase the upper limit if necessary with 'http-wordpress-users.limit'
| vulners:
|   cpe:/a:apache:http_server:2.4.29:
|     	CVE-2019-0211	7.2	https://vulners.com/cve/CVE-2019-0211
|     	CVE-2018-1312	6.8	https://vulners.com/cve/CVE-2018-1312
|     	CVE-2017-15715	6.8	https://vulners.com/cve/CVE-2017-15715
<SNIP>
```
