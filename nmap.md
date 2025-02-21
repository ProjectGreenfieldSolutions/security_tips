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
