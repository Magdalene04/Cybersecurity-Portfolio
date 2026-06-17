## TryHackMe CTF : Crack The Hash - Level 1
The Crack the Hash CTF is using hash cracking tools to crack the hash and find the original data.

There are two levels in this Level 1 CTF itself. Let's go through the first one.

## Tools Used
### Hashcat:
Hashcat tool is a powerful, open-source password recovery tool optimized for incredible speed by utilizing GPU parallel processing.

### John the Ripper:
John the Ripper is a highly flexible, CPU-based password cracking tool renowned for its ability to automatically detect hash formats and apply custom rulesets.

### Crackstation
Crackstation is a web-based lookup service that leverages massive, pre-computed rainbow tables to crack non-salted hashes instantly.

## Level 1
### 1) Crack the hash "48bb6e862e54f2a795ffc4e541caed4d"
To crack the hash, we need to first understand what format of hash this is. To understand that I'm going to use **Hashcat** tool. 

```bash
echo '48bb6e862e54f2a795ffc4e541caed4d' > hash1.txt
hashcat --show hash1.txt
```

After knowing the format of the hash, I'm going to use John The Ripper to crack the hash. Hashcat tool can also be used, but I prefer John The Ripper for Level 1.

```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt
```
By doing so we got to know the format of hash is **MD5** and also cracked the hash. The output for the hash 48bb6e862e54f2a795ffc4e541caed4d is **easy.**

<img width="1919" height="758" alt="image" src="https://github.com/user-attachments/assets/082a08b3-f847-419a-a37f-8de64563489b" />

### 2) Crack the hash "CBFDAC6008F9CAB4083784CBD1874F76618D2A97"
We will be applying the above method to crack all the hashes in Level 1.

```bash
echo 'CBFDAC6008F9CAB4083784CBD1874F76618D2A97' > hash2.txt
hashcat --show hash2.txt
john --format=raw-sha1 --wordlist=/usr/share/worlists/rockyou.txt hash2.txt
```
The format of the hash is **SHA-1** and the output for the hash CBFDAC6008F9CAB4083784CBD1874F76618D2A97 is **password123.**

<img width="1900" height="743" alt="image" src="https://github.com/user-attachments/assets/900cdabc-2193-4993-9614-dbb63fa23ea2" />

### 3) Crack the hash "1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032"

```bash
echo '1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032' > hash3.txt
hashcat --show hash3.txt
john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash3.txt
```
The format of the hash is **SHA2-256" and the output for the hash 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 is **letmein.**

<img width="1886" height="742" alt="image" src="https://github.com/user-attachments/assets/97599feb-fade-47c1-86d6-3e1faa23854f" />

### 4) Crack the hash "$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom"

```bash
echo '$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom' > hash4.txt
hashcat --show hash4.txt
```

We got the format as **bcrypt.** bcrypt hashes take a lot of time to crack so instead of using the above ways we will do something different.
<img width="1896" height="668" alt="Screenshot 2026-06-17 185419" src="https://github.com/user-attachments/assets/cb873914-1f95-4741-8b60-623361e02762" />

We got an hint like "This type of hash can take a very long time to crack, so either filter rockyou for four character words, or use a mask for four lower case alphabetical characters."
So based on this lets try to work. I will filter out all four letter words in rockyou.txt and redirect the output to filtered_wordlist.txt

```bash
grep -x '.\{4\}' /usr/share/wordlists/rockyou.txt > /usr/share/wordlists/filtered_wordlist.txt
cat filtered_wordlist.txt
john --format=bcrypt --wordlist=/usr/share/wordlists/filtered_wordlist.txt hash4.txt
```
<img width="1898" height="520" alt="image" src="https://github.com/user-attachments/assets/db55e6c0-201d-4d81-99ad-c72e0bbca999" />

The output from the hash is **bleh.**

## 5) Crack the hash "279412f945939ba78ce0758d3fd83daa"

```bash
echo '279412f945939ba78ce0758d3fd83daa' > hash5.txt
hashcat --show hash5.txt
john --format=raw-md4 --wordlist=/usr/share/wordlists/rockyou.txt hash5.txt
```

We got the output as exhausted meaning the password is not in the list. So we will use an online available tool to see if its a known hash. We will use Crackstation to o so.

<img width="1900" height="690" alt="image" src="https://github.com/user-attachments/assets/cc56c89c-3fd9-4f41-952e-f6dbf4247639" />

The output we got for this hash is **Eternity22.**

---
## Level 2: 
### 6) Crack the hash "F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85"

```bash
echo 'F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85' > hash6.txt
hashcat --show hash6.txt
john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash6.txt
```
<img width="1901" height="729" alt="image" src="https://github.com/user-attachments/assets/cbd90100-d668-4fbf-b062-d8c77b83b0b1" />

The cracked hash is **paule.**

### 7) Crack the hash "1DFECA0C002AE40B8619ECF94819CC1B"

```bash
echo '1DFECA0C002AE40B8619ECF94819CC1B' > hash7.txt
hashcat --show hash7.txt
john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hash7.txt
```

MD4, MD5 were given first, but both were not right and hash didn't get cracked. Next, I used nt format for NTLM and got the hash cracked which is **n63umy8lkf4i.**

<img width="1910" height="845" alt="Screenshot 2026-06-17 215505" src="https://github.com/user-attachments/assets/9d4c155d-4b8f-4ea7-b8b7-bf85afa298e7" />

### 8) Crack the hash "$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02." 
### Salt: aReallyHardSalt

```bash
echo '$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.' > hash8.txt
hashcat --show hash8.txt
hashcat -m 1800 -a 0 hash8.txt /usr/share/wordlists/rockyou.txt
```
This hash format is SHA512crypt, hence having the salt in the beginning in between $6$ and $. We have used hashcat to crack as john the ripper is not compatible
<img width="1906" height="748" alt="image" src="https://github.com/user-attachments/assets/977ffe27-6e31-4569-ad8a-67d5f0b6801a" />

### 9) Crack the hash "e5d8870e5bdd26602cab8dbe07a942c8669e56d6" Salt: tryhackme

```bash
echo 'e5d8870e5bdd26602cab8dbe07a942c8669e56d6:tryhackme' > hash9.txt
hashcat --show hash9.txt
hashcat -m 160 -a 0 hash9.txt /usr/share/wordlists/rockyou.txt
```
Since this is a SHA-1 hash, we will add the salt at the end of the hash. I have used hashcat to crack this because John The Ripper has limited its capability.
<img width="1919" height="630" alt="image" src="https://github.com/user-attachments/assets/a0d307d8-7d66-463f-a872-212f34fc3700" />

<img width="1876" height="664" alt="image" src="https://github.com/user-attachments/assets/c47908bb-9d01-40d0-a8cd-613a911b1154" />

<img width="1853" height="751" alt="image" src="https://github.com/user-attachments/assets/289de20f-faf1-4b1f-8033-bfa6edede441" />

---
## What I Learned:
**The Importance of Salts:** Walking through Level 2 heavily reinforced how cryptographic salts completely neutralize fast lookup methods like CrackStation. Without a salt, a complex password hashed in MD4 can be broken instantly via rainbow tables; with a custom salt, local dictionary attacks are strictly required.

**Tool Adaptability:** I learned that real-world password cracking isn't a one-size-fits-all process. Shifting from John the Ripper to Hashcat when encountering specific constraints (like JTR's limitations with certain SHA-1 implementations or SHA512crypt performance) taught me to dynamically choose the right tool based on the target algorithm.

**Troubleshooting Formats:** Investigating failed cracks (like in Task 7) taught me the value of analyzing the context of a hash. Realizing that standard MD4/MD5 formats failed, and pivoting to the NTLM (nt) structure based on target environment clues, highlighted the critical role that reconnaissance plays in cryptography.
