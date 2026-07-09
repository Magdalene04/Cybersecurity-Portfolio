# NMAP - The Basics
Nmap stands for Network Mapper. This tool allows us to scan networks to identify open ports, devices, OS Detection, Service Versions etc. It also allows us to find vulnerabilities using NMAP Script Engine.

## Learning Objectives
* Discover live hosts
* Find running services on the live hosts
* Distinguish the different types of port scans
* Detect the versions of the running services
* Control the timing
* Format the output

## Host Discovery: Who is online
* IP range using -: If you want to scan all the IP addresses from 192.168.0.1 to 192.168.0.10, you can write 192.168.0.1-10
* IP subnet using /: If you want to scan a subnet, you can express it as 192.168.0.1/24, and this would be equivalent to 192.168.0.0-255
* Hostname: You can also specify your target by hostname, for example, example.thm

Let’s say you want to discover the online hosts on a network. Nmap offers the **-sn** option, i.e., ping scan. However, don’t expect this to be limited like ping. 

### Scanning a Local Network
This means that you can scan the targets in the same network such as Ethernet or Wi-Fi. We will get the available device's MAC Address.

### Scanning a Remote Network
Scanning public networks with two or more routers. Atleast one router separates our network from the other networks. Here, we can use ARP to send request and receive responses.

**ARP Scan** - This scan allows you to scan for devices in the same network. <br>
**Command** : arp-scan

Nmap offers a list scan with the option -sL. This scan only lists the targets to scan without actually scanning them. For example, nmap -sL 192.168.0.1/24 will list the 256 targets that will be scanned. This option helps confirm the targets before running the actual scan.

#### Questions
1) What is the last IP address that will be scanned when your scan target is 192.168.0.1/27? <br>
**Ans:** 192.168.0.31

**Explanation**: So /27 subnet has 32 hosts. Two IP's are reserved for Network and Broadcast IP. That makes it 30 hosts. Since we are scanning all targets under 32 hosts range from 0-31, the last IP to be scanned will be 31. Hence, 192.168.0.31

## Port Scanning: Who is Listening?
We have TCP and UDP ports that can be scanned. Each one is used for different purpose. TCP is for reliable connection for communication wheras UDP is used for Live Streaming, Online Games etc.

### TCP Connect Scan:
* Full open scan
* Establishes connection to the target
* Uses three-way handshake (SYN, SYN/ACK, ACK)
* Find only TCP port and not UDP
* High chances of getting logged.

**Command**: nmap -sT <target-ip>

### TCP SYN Scan: (Stealth scan)
* Half-open scanning
* Sends SYN packets to the target
* Won't create a session
* Fast and Reliable
* Less possibility of getting logged.

**Command**: nmap -sS <target-ip>

## UDP Port Scan:
* Slowest scanning technique of all
* Find's only UDP ports
* Does not require establishing a connection and tearing it down afterwards
* Suitable for real-time communication, such as live broadcasts

**Command**: nmap -sU <target-ip>

### Limiting the Target Ports
Nmap scans the most common 1,000 ports by default. However, this might not be what we are looking for. Therefore, Nmap offers a few more options.

* -F is for Fast mode, which scans the 100 most common ports (instead of the default 1000).
* -p[range] allows us to specify a range of ports to scan. For example, -p10-1024 scans from port 10 to port 1024, while -p-25 will scan all the ports between 1 and 25. Note that -p- scans all the ports and is equivalent to -p1-65535 and is the best option if we want to be as thorough as possible.
* **Tip:** The most common services use a port number between 1 and 1024 for either UDP or TCP. These ports are also known as well-known ports. Use -p1-1023 to scan for the well-known ports.

### Summary 

| Option | Explanation |
| :--- | :--- |
| `-sT` | TCP connect scan – complete three-way handshake |
| `-sS` | TCP SYN – only first step of the three-way handshake (Stealth) |
| `-sU` | UDP scan |
| `-F` | Fast mode – scans the 100 most common ports |
| `-p[range]` | Specifies a range of port numbers – `-p-` scans all 65,535 ports |

#### Questions
1) How many TCP ports are open on the target system at 10.49.167.75? <br>
**Ans:** 6

<img width="1137" height="387" alt="image" src="https://github.com/user-attachments/assets/8f78166c-6e0d-4bbd-85db-60bdd6d7da91" />

2) Find the listening web server on 10.49.167.75 and access it with your browser. What is the flag that appears on its main page? <br>
**Ans:** THM{SECRET_PAGE_38B9P6}

<img width="1890" height="581" alt="image" src="https://github.com/user-attachments/assets/91d8af28-2096-46f5-964f-9f0366967a7c" />

## Version Detection: Extract More Information
### OS Detection
You can enable OS detection by adding the -O option. he OS detection option triggers Nmap to rely on various indicators to make an educated guess about the target OS. However, there is no perfectly accurate OS detector. 

### Service and Version Detection
-sV enables version detection. This is very convenient for gathering more information about the target's service versions.

To use both -O and -sV we can use **Aggressive Scan -A**. It gives both these details and additional more informations.

### Summary

| Option | Explanation |
| :--- | :--- |
| `-O` | OS detection |
| `-sV` | Service and version detection |
| `-A` | OS detection, version detection, and other additions |
| `-Pn` | Scan hosts that appear to be down |

#### Question
1) What is the name and detected version of the web server running on 10.49.167.75? <br>
**Ans:** lighttpd 1.4.74

<img width="1914" height="657" alt="image" src="https://github.com/user-attachments/assets/a8a8b12f-65e6-4d3e-9346-c225849c104b" />

## Timing: How fast is fast
Running the scan at its normal speed might trigger an IDS or other security solutions. It is reasonable to control how fast a scan should go. Nmap gives six timing templates: **paranoid (0), sneaky (1), polite (2), normal (3), aggressive (4), and insane (5)**. We can pick the timing template by its name or number. For example, we can add -T0 (or -T 0) or -T paranoid to opt for the slowest timing.

**Note**: Don't stress the target as a pentester

| Option | Explanation |
| :--- | :--- |
| `-T<0-5>` | Timing template – paranoid (0), sneaky (1), polite (2), normal (3), aggressive (4), and insane (5) |
| `--min-parallelism <numprobes>` and `--max-parallelism <numprobes>` | Minimum and maximum number of parallel probes |
| `--min-rate <number>` and `--max-rate <number>` | Minimum and maximum rate (packets/second) |
| `--host-timeout <time>` | Maximum amount of time to wait for a target host |

#### Question
1) What is the non-numeric equivalent of -T4? <br>
**Ans:** -T Aggressive

## Output: Controlling what you see
This has two main features

* Showing additional information while a scan takes place
* Choosing the file format to save the scan report

### Verbosity and Debugging
In some cases, the scan takes a very long time to finish or to produce any output that will be displayed on the screen. Sometimes we might be interested in more real-time information about the scan progress. The best way to get more updates about what’s happening is to enable verbose output by adding **-v**.

We can increase the verbosity level by adding another “v” such as -vv or even -vvvv. We can also specify the verbosity level directly, for example, -v2 and -v4. We can even increase the verbosity level by pressing “v” after the scan already started.

If all this verbosity does not satisfy our needs, we must consider the -d for debugging-level output. Similarly, we can increase the debugging level by adding one or more “d” or by specifying the debugging level directly. The maximum level is -d9; before choosing that, we must be ready for thousands of information and debugging lines.

### Saving Scan Report:
After finishing the scanning, we might need to save the output in a file. NMAP allows us to save the output in different formats:

* -oN <filename> - Normal output
* -oX <filename> - XML output
* -oG <filename> - grep-able output (useful for grep and awk)
* -oA <basename> - Output in all major formats

#### Question
1) What option must you add to your nmap command to enable debugging?
**Ans:** -d

## Conclusion
It is best to run Nmap with sudo privileges so that we can make use of all its features. Running Nmap with local user privileges will still work; however, we should expect many features to be unavailable. We get a minimal portion of Nmap’s power when running it as a local user. For instance, Nmap would automatically use SYN scan (-sS) if we are running it with sudo privileges and will default to connect scan (-sT) if run as a local user. The reason is that crafting certain packets, such as sending a TCP SYN packet, requires root privileges.

#### Question
1) What kind of scan will Nmap use if you run nmap MACHINE_IP with local user privileges? <br>
**Ans:** Connect Scan


