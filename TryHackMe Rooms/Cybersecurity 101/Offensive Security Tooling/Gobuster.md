# TryHackMe: Gobuster: The Basics
# Gobuster: The Basics

## Introduction
Gobuster is an open-source offensive security tool written in Golang used for enumerating hidden web directories, subdomains, VHOSTs, and cloud storage buckets. It leverages targeted wordlists and brute-force techniques to analyze server responses during reconnaissance and scanning phases.

* **Enumeration:** The practice of systematically identifying and listing all available resources or endpoints on a target, regardless of whether they are publicly linked.
* **Brute Force:** The process of testing every entry from a wordlist sequentially against a server until matching responses are identified.

---

## Overview

### Usage
```bash
gobuster [command] [flags]
```

### Key Available Commands
* `dir` – Performs web directory and file enumeration mode.
* `dns` – Performs DNS subdomain enumeration mode.
* `vhost` – Performs virtual host (VHOST) enumeration mode.

### Common Flags
* `-u`, `--url`: Specifies the target URL or domain.
* `-w`, `--wordlist`: Sets the path to the wordlist file used for brute-forcing.
* `-t`, `--threads`: Defines the number of concurrent threads (default is 10).
* `-o`, `--output`: Saves the scan results directly to a designated file.
* `-r`, `--follow-redirect`: Forces Gobuster to follow HTTP redirects.
* `-x`, `--extensions`: Specifies file extensions to append to wordlist entries (e.g., `php,html,txt`).

---

## Command Examples & Explanations

### Example 1: Standard Directory Scan with Threads
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirb/small.txt -t 64
```

* **`gobuster dir`**: Sets the execution mode to directory and file enumeration.
* **`-u "http://www.example.thm/"`**: Specifies the target URL to scan.
* **`-w /usr/share/wordlists/dirb/small.txt`**: Directs Gobuster to use the `small.txt` wordlist to generate URI path requests.
* **`-t 64`**: Increases the concurrent thread count to 64 to process requests significantly faster.

## Questions:
**1) What flag do we use to specify the target URL?** <br>
**Ans:** -u

**2) What command do we use for the subdomain enumeration mode?** <br>
**Ans:** dns

## Use Case: Directory and File Enumeration

### Key `dir` Command Flags
* `-c`, `--cookies`: Configures a cookie string (such as session IDs) to send with each request.
* `-x`, `--extensions`: Specifies file extensions to search for (e.g., `php,js,txt`).
* `-H`, `--headers`: Specifies custom headers to include with each request.
* `-k`, `--no-tls-validation`: Skips TLS/SSL certificate verification (useful for self-signed CTF targets).
* `-n`, `--no-status`: Disables printing response status codes to keep terminal output clean.
* `-s`, `--status-codes`: Sets specific HTTP status codes to display (e.g., `200,204,301`).
* `-b`, `--status-codes-blacklist`: Excludes specified HTTP status codes from the output.
* `-r`, `--follow-redirect`: Forces Gobuster to follow HTTP redirect responses (`301`, `302`).

---

### How to Use `dir` Mode
The `dir` mode is used to discover hidden directories and files on a web server by testing words from a specified list against the base URL. 

To run a basic directory scan, use the required `-u` (URL) and `-w` (wordlist) flags:

### Example 1: Following Redirects
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirb/small.txt -r
```

* **`gobuster dir`**: Retains directory enumeration mode.
* **`-u "http://www.example.thm/"`**: Sets the target web server URL.
* **`-w /usr/share/wordlists/dirb/small.txt`**: Points to the target wordlist.
* **`-r`**: Replaces the thread parameter to instruct Gobuster to automatically follow HTTP redirects (such as `301` or `302` response status codes).

### Example 2: Following Redirects
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirb/small.txt -x
```

* **`gobuster dir`**: Executes directory and file discovery.
* **`-u "http://www.example.thm/"`**: Sets the target URL base.
* **`-w /usr/share/wordlists/dirb/small.txt`**: Points to the wordlist file.
* **`-x php,html,txt`**: Appends `.php`, `.html`, and `.txt` extensions to every term in the wordlist to search for specific file types alongside directory names.

#### Important Considerations
* **Required Protocol:** The `-u` flag must always include the protocol (`http://` or `https://`).
* **Non-Recursive Scanning:** Gobuster does not automatically scan subdirectories. If a directory like `/admin` is discovered, you must execute a separate scan targeting `http://www.example.thm/admin/` to enumerate its internal contents.
* **Target Specifier:** Using hostnames instead of raw IP addresses ensures request routing reaches the intended virtual host when multiple sites share a single IP address.

## Questions:
**1) Which flag do we have to add to our command to skip the TLS verification? Enter the long flag notation.**<br>
**Ans:** --no-tls-validation

**2) Enumerate the directories of www.offensivetools.thm. Which directory catches your attention?**<br>
**Ans:** secret

<img width="1799" height="771" alt="image" src="https://github.com/user-attachments/assets/4c28cab2-b078-40fd-be20-11064d05f171" />
<img width="1184" height="220" alt="image" src="https://github.com/user-attachments/assets/04f086e8-e36d-40d8-a31f-055da3fe3712" />

**3) Continue enumerating the directory found in question 2. You will find an interesting file there with a .js extension. What is the flag found in this file?** <br>
**Ans:** THM{ReconWasASuccess}

<img width="1888" height="738" alt="image" src="https://github.com/user-attachments/assets/c627db15-90d6-4cc3-8738-fbbf56fa7f95" />

## Use Case: Subdomain Enumeration

### Key `dns` Command Flags
* `-d`, `--domain`: Specifies the target domain to enumerate subdomains for (e.g., `example.thm`).
* `-w`, `--wordlist`: Path to the wordlist containing common subdomain names.
* `-r`, `--resolver`: Uses a custom DNS server for address resolution (e.g., `1.1.1.1` or `8.8.8.8`).
* `-c`, `--show-cname`: Displays CNAME records alongside resolved IP addresses.
* `-i`, `--show-ips`: Shows resolved IP addresses for discovered subdomains.
* `--wildcard`: Forces Gobuster to continue scanning even if wildcard DNS resolution is detected.

---

### How to Use `dns` Mode
The `dns` mode uses DNS brute-forcing to discover existing subdomains by appending entries from a wordlist to the target domain and attempting to resolve them.

To run a basic subdomain scan, pass the domain using `-d` and your wordlist using `-w`:

```bash
gobuster dns -d "example.thm" -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

#### Important Considerations
* **No Protocol Needed:** Unlike `dir` mode, the `-d` flag requires a raw domain name (e.g., `example.thm`), not a URL with `http://` or `https://`.
* **DNS Resolution Speed:** Subdomain enumeration relies on sending DNS queries. Using public resolvers (like Cloudflare's `1.1.1.1`) via the `-r` flag can often improve query speeds.
* **Wildcard Detection:** If a domain resolves all non-existent subdomains to a single fallback IP, Gobuster will report wildcard DNS. Use the `--wildcard` flag to bypass this check if necessary.
  
## Questions
**1) Apart from the dns keyword and the -w flag, which shorthand flag is required for the command to work?** <br>
**Ans:** -d

**2) Use the commands learned in this task, how many subdomains are configured for the offensivetools.thm domain?** <br>
**Ans:** 4

<img width="1812" height="684" alt="image" src="https://github.com/user-attachments/assets/ae82fe7f-a409-4847-a654-c42a0b31783a" />

## Use Case: Vhost Enumeration

### Key `vhost` Command Flags
* `-u`, `--url`: Specifies the base URL or target IP address for brute-forcing virtual hosts.
* `-w`, `--wordlist`: Path to the wordlist containing potential hostnames/subdomains.
* `--domain`: Appends the specified root domain to form valid target hostnames (e.g., `example.thm`).
* `--append-domain`: Appends the configured domain name directly to each wordlist entry.
* `-m`, `--method`: Specifies the HTTP method to use for requests (e.g., `GET`, `POST`).
* `--exclude-length`: Excludes specific response body lengths from the output to filter out false positives.
* `-r`, `--follow-redirect`: Forces Gobuster to follow HTTP redirects.

---

### How to Use `vhost` Mode
The `vhost` mode is used to discover virtual hosts running on the target server. Unlike DNS enumeration, VHOST enumeration sends HTTP requests directly to the target IP address or URL while dynamically changing the `Host:` header in each request.

To run a basic virtual host scan, supply the target URL or IP address with `-u`, set the wordlist with `-w`, specify the target domain with `--domain`, append the domain using `--append-domain`, and filter out noise using `--exclude-length`:

```bash
gobuster vhost -u "[http://10.10.10.10](http://10.10.10.10)" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```

#### Important Considerations
* **Virtual Hosts vs. Subdomains:** Virtual hosts are hosted on the same physical server/IP address and rely on the HTTP `Host:` header for routing, whereas subdomains rely on public or internal DNS server resolution.
* **Filtering False Positives:** Target web servers often return uniform error pages (such as `404 Not Found` or fallback default pages) for non-existent virtual hosts. Using `--exclude-length` allows you to hide those uniform response sizes and isolate legitimate vhosts.
* **Using `--append-domain`:** Omitting `--append-domain` causes Gobuster to send raw wordlist terms in the `Host:` header (e.g., `Host: admin`) instead of complete domain structures (e.g., `Host: admin.example.thm`), which can produce inaccurate results or high volumes of false positives.

**Questions**
**1) Use the commands learned in this task to answer the following question: How many vhosts on the offensivetools.thm domain reply with a status code 200?** <br>
**Ans:** 4

<img width="1919" height="726" alt="image" src="https://github.com/user-attachments/assets/31a5c2c9-cd72-4cfe-985e-d79a8d255ee5" />

## Conclusion

This room introduced **Gobuster**, a powerful command-line offensive security tool written in Go, essential for the enumeration phase of a security assessment. By performing high-speed brute-force attacks against target servers using customizable wordlists, Gobuster helps uncover unlinked endpoints, hidden files, and internal subdomains.

Key topics and modes covered include:

* **`dir` Mode:** Enumerates hidden web directories and files by sending HTTP GET requests across generated path patterns.
* **`dns` Mode:** Discovers valid subdomains by sending DNS resolution queries using a wordlist and target domain name.
* **`vhost` Mode:** Identifies virtual hosts running on the same IP address by altering the HTTP `Host:` header in direct web requests to the server.

---

### Core Takeaways & Differences
* **DNS vs. VHOST Enumeration:** DNS mode relies on resolving hostnames via DNS servers, while VHOST mode directly queries the web server's host routing behavior.
* **Fine-Tuning Scans:** Using specific flags such as `-x` (file extensions), `--exclude-length` (filtering response sizes), and `-r` (following redirects) helps reduce false positives and deliver precise results.

