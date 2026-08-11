# TryHackMe: Hacker Holidays 2026 Pathway

## 🏅 Certification Overview
I completed the 14-day *Hacker Holidays 2026* event on TryHackMe, solving all 14 challenges across the resort map. Each day tested hands-on offensive security, web exploitation, cloud security, forensics, and AI prompt engineering.
- *Issued By:* TryHackMe
- *Focus Areas:* AWS IAM & Cloud Authorization, NoSQL & SSTI, AI Prompt Injection, Unsafe Deserialization, Race Conditions, Forensics, and Privilege Escalation

<img width="1258" height="746" alt="Screenshot 2026-08-12 002143" src="https://github.com/user-attachments/assets/d3d7e626-e176-4763-8e98-2a74ac08c756" />

## 🧠 Room-by-Room Key Domains & Hands-on Lab Mastery

### Day 1: The Concierge Knows Too Much
- *What I Did:* Interacted with the AI resort concierge (VERA) and executed indirect prompt injection to bypass guardrails and reveal restricted administrative memory.
- *Practical Application:* Isolated user prompt inputs from privileged system instructions and context boundaries to prevent unauthorized function execution.

### Day 2: Room 404
- *What I Did:* Discovered hidden endpoints and manipulated web server request routing to bypass 404/403 restrictions and access forbidden internal admin directories.
- *Practical Application:* Configured secure server routing rules and eliminated client-side URL trust to enforce backend access control checks.

### Day 3: Complimentary
- *What I Did:* Analyzed public APIs to uncover unauthenticated endpoints exposing sensitive guest data and complimentary resort vouchers.
- *Practical Application:* Implemented strict token-based authentication (JWT/OAuth2) on all backend API endpoints to prevent broken object-level authorization (BOLA).

### Day 4: Packed Light
- *What I Did:* Audited exposed `.git` metadata directories on the web server, dumped repository objects, and reconstructed source code to extract hardcoded API keys.
- *Practical Application:* Restricted web server access to hidden metadata directories (`/.git/`) and sanitized repository commit history before production deployment.

### Day 5: Beach Bar
- *What I Did:* Identified over-privileged unauthenticated AWS Cognito roles granting unrestricted `dynamodb:Scan` access, allowing cross-tenant data retrieval.
- *Practical Application:* Applied Fine-Grained Access Control (FGAC) in IAM policies using `dynamodb:LeadingKeys` bound to `${cognito-identity.amazonaws.com:sub}`.

### Day 6: Overheard at Breakfast
- *What I Did:* Extracted OSINT clues from overheard conversations and performed email hash enumeration (MD5/SHA256) across public platforms to locate hidden user profiles.
- *Practical Application:* Enforced privacy controls on public profile bios and sanitized string inputs prior to hashing operations.

### Day 7: Do Not Disturb
- *What I Did:* Bypassed login authentication using NoSQL injection (`[$ne]`) in Node.js/Express and leveraged Server-Side Template Injection (SSTI) in EJS for initial access.
- *Practical Application:* Implemented strict input typing/schema validation and secured local Node.js debugging ports (`9229`) against host privilege escalation.

### Day 8: Towel on the Sunbed
- *What I Did:* Exploited race conditions in the resort booking application by manipulating concurrent request bursts to double-book limited sunbeds.
- *Practical Application:* Implemented atomic database transactions and concurrency locks (mutexes) to maintain strict state consistency under load.

### Day 9: CryptoCabana
- *What I Did:* Analyzed weak cryptographic implementations and predictable key generation algorithms in the guest portal to decrypt protected session tokens.
- *Practical Application:* Replaced custom or weak cipher suites with standard, securely seeded cryptographic libraries (AES-GCM with CSPRNG).

### Day 10: The Hollow Shell
- *What I Did:* Exploited insecure YAML deserialization (`yaml.load`) in python backend services to execute arbitrary system commands and spawn a reverse shell.
- *Practical Application:* Replaced hazardous deserialization functions with safe parsers (`yaml.safe_load`) and removed cleartext credentials from process listings.

### Day 11: Infinity Pool
- *What I Did:* Conducted network traffic analysis on PCAP files from the pool area's Wi-Fi network to detect covert C2 beacons and decrypt exfiltrated guest payloads.
- *Practical Application:* Utilized Wireshark display filters and IDS signatures to identify data exfiltration over non-standard protocols.

### Day 12: After Hours
- *What I Did:* Identified local privilege escalation vectors on the Linux target by exploiting misconfigured SUID binaries and insecure cron jobs.
- *Practical Application:* Applied the principle of least privilege, removed unnecessary SUID permissions, and secured root-executed maintenance scripts.

### Day 13: The Guestbook
- *What I Did:* Discovered Stored Cross-Site Scripting (XSS) in the resort guestbook feature and hijacked administrative session cookies to compromise admin accounts.
- *Practical Application:* Implemented contextual output encoding, robust Content Security Policies (CSP), and set the `HttpOnly` flag on sensitive cookies.

### Day 14: Management Wants a Word
- *What I Did:* Executed a full multi-stage attack chain—combining OSINT, cloud misconfigurations, web injections, and privilege escalation—to achieve full root compromise of resort infrastructure.
- *Practical Application:* Applied defense-in-depth security controls across web frontend, API endpoints, cloud IAM policies, and underlying host systems.


## 🚀 How This Benefits My Portfolio
Successfully completing all 14 rooms in order, demonstrated my end-to-end technical capabilities in cloud security, web exploitation, digital forensics, and AI prompt defense—reflecting real-world adversarial methodologies and actionable remediation skills.
