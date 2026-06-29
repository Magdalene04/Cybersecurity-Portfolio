# NMAP
Nmap

There are totally 65535 ports ranging from 0 to 65354, in which 1024 ports ranging from 0 - 1023 are well-known standard ports.

## Introduction
Questions:
1) What networking constructs are used to direct traffic to the right application on a server?<br>
**Ports**

2) How many of these are available on any network-enabled computer? <br>
**65535**
   
3) How many of these are considered "well-known"? <br>
**1024**

## Nmap Switches
Switches are command arguments which tells a program to do different things.

Nmap has two flags to mention its uses. The -h flag (help) gives the main commands of nmap and the man command gives the detailed information on nmap.

```bash
nmap -h
man nmap
```

Questions:
1) What is the first switch listed in the help menu for a 'Syn Scan'? <br>
**-sS**

2) Which switch would you use for a "UDP scan"? <br>
**-sU**

3) If you wanted to detect which operating system the target is running on, which switch would you use? <br>
**-O**

4) Nmap provides a switch to detect the version of the services running on the target. What is this switch? <br>
**-sV**
   
5) The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity?<br>
**-v**

6) Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two? <br>
**-vv**

7) We should always save the output of our scans -- this means that we only need to run the scan once (reducing network traffic and thus chance of detection), and gives us a reference to use when writing reports for clients. What switch would you use to save the nmap results in three major formats?<br>
**-oA**

8) What switch would you use to save the nmap results in a "normal" format? <br>
**-oN**

9) A very useful output format: how would you save results in a "grepable" format? <br>
**-oG**

10) Sometimes the results we're getting just aren't enough. If we don't care about how loud we are, we can enable "aggressive" mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning. How would you activate this setting?<br>
**-A**

11) Nmap offers five levels of "timing" template. These are essentially used to increase the speed your scan runs at. Be careful though: higher speeds are noisier, and can incur errors! How would you set the timing template to level 5?<br>
**-T5**

12) We can also choose which port(s) to scan. How would you tell nmap to only scan port 80? <br>
**-p 80**

13) How would you tell nmap to scan ports 1000-1500? <br>
**-p 1000-1500**

14) A very useful option that should not be ignored: How would you tell nmap to scan all ports? <br>
**-p-**

15) How would you activate a script from the nmap scripting library? <br>
**--script**

16) How would you activate all of the scripts in the "vuln" category? <br>
**--script=vuln**

## Scan Types Overview
When port scanning with Nmap, there are three basic scan types. These are:

TCP Connect Scans (-sT) <br>
SYN "Half-open" Scans (-sS) <br>
UDP Scans (-sU) <br>

Additionally there are several less common port scan types. These are:

TCP Null Scans (-sN) <br>
TCP FIN Scans (-sF) <br>
TCP Xmas Scans (-sX) <br>

## TCP Connect Scan
A TCP Connect scan works by performing the three-way handshake with each target port in turn. In other words, Nmap tries to connect to each specified TCP port, and determines whether the service is open by the response it receives. 

If a port is closed, the RFC 9293 states that the server will send back a reset packet.

A TCP three-way handshake is where the client sends a SYN packet to the server to see for connection. If the server is open, it will send back a SYN+ACK packet to the client. The client will again send back a ACK package to establish the communication and to complete the handshake.

If the server is closed, after the SYN packet is sent, the server will send back a RST packet which indicates it is closed to nmap.

What if the port is open, but hidden behind a firewall?

Many firewalls are configured to simply drop incoming packets. Nmap sends a TCP SYN request, and receives nothing back. This indicates that the port is being protected by a firewall and thus the port is considered to be **filtered**.

That said, it is very easy to configure a firewall to respond with a RST TCP packet. For example, in IPtables for Linux, a simple version of the command would be as follows:

```bash
iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset
```

This can make it extremely difficult (if not impossible) to get an accurate reading of the target(s).

Questions:
1) Which RFC defines the appropriate behaviour for the TCP protocol? <br>
**RFC 9293**

2) If a port is closed, which flag should the server send back to indicate this? <br>
**RST**

## SYN Scans
SYN scans (-sS) are used to scan the TCP port-range of a target or targets; however, the two scan types work slightly different. <br>
SYN scans are sometimes referred to as **"Half-open"** scans, or **"Stealth"** scans. <br>
Where TCP scans perform a full three-way handshake with the target, SYN scans sends back a RST TCP packet after receiving a SYN/ACK from the server. This prevents the server from repeatedly trying to make the request. <br>

SYN scans can be only run in **sudo** permissions because it should generate its own raw packet. If no sudo permissions, then the default TCP scan runs.

Questions:
1) There are two other names for a SYN scan, what are they? <br>
**Half-open, stealth**

2) Can Nmap use a SYN scan without Sudo permissions (Y/N)? <br>
**N**

## UDP Scans
Unlike TCP, UDP connections are stateless. This means that, rather than initiating a connection with a back-and-forth "handshake", UDP connections rely on sending packets to a target port and essentially hoping that they make it. This makes UDP superb for connections which rely on speed over quality (e.g. video sharing), but the lack of acknowledgement makes UDP significantly more difficult (and much slower) to scan. The switch for an Nmap UDP scan is (-sU)

When a packet is sent to an open UDP port, there should be no response. When this happens, Nmap refers to the port as being open|filtered. In other words, it suspects that the port is open, but it could be firewalled. If it gets a UDP response (which is very unusual), then the port is marked as open. More commonly there is no response, in which case the request is sent a second time as a double-check. If there is still no response then the port is marked open|filtered and Nmap moves on.

When a packet is sent to a closed UDP port, the target should respond with an ICMP (ping) packet containing a message that the port is unreachable. This clearly identifies closed ports, which Nmap marks as such and moves on.

Questions:
1) If a UDP port doesn't respond to an Nmap scan, what will it be marked as? <br>
**open|filtered**

2) When a UDP port is closed, by convention the target should send back a "port unreachable" message. Which protocol would it use to do so? <br>
**ICMP**

## NULL, FIN and Xmas Scans
NULL scans (-sN) are when the TCP request is sent with no flags set at all. As per the RFC, the target host should respond with a RST if the port is closed.<br>
FIN scans (-sF) work in an almost identical fashion; however, instead of sending a completely empty packet, a request is sent with the FIN flag (usually used to gracefully close an active connection). Once again, Nmap expects a RST if the port is closed. <br>
Xmas scans (-sX) send a malformed TCP packet and expects a RST response for closed ports. It's referred to as an xmas scan as the flags that it sets (PSH, URG and FIN) give it the appearance of a blinking christmas tree when viewed as a packet capture in Wireshark.

The expected response for open ports with these scans is also identical, and is very similar to that of a UDP scan. If the port is open then there is no response to the malformed packet. Unfortunately (as with open UDP ports), that is also an expected behaviour if the port is protected by a firewall, so NULL, FIN and Xmas scans will only ever identify ports as being open|filtered, closed, or filtered. If a port is identified as filtered with one of these scans then it is usually because the target has responded with an ICMP unreachable packet.

Questions:
1) Which of the three shown scan types uses the URG flag? <br>
**Xmas**

2) Why are NULL, FIN and Xmas scans generally used? <br>
**Firewall Evasion**

3) Which common OS may respond to a NULL, FIN or Xmas scan with a RST for every port? <br>
**Microsoft Windows**

## ICMP Network Scanning


