### TryHackMe CTF: Pickle Rick

This Rick and Morty-themed challenge requires us to exploit a web server and find three ingredients to help Rick make his potion and transform himself back into a human from a pickle.

## Step 1: Deploy the website
Using the IP Address 10.48.145.44 given in the CTF Room, I did nmap scan first to see what all ports are open.

<img width="1323" height="524" alt="image" src="https://github.com/user-attachments/assets/59197766-1c0a-4d5a-bb92-2fc7490abed8" />

We got two open ports ssh and http. But we don't have any credentials now to access ssh, so lets try opening the website with the given IP.

<img width="1919" height="849" alt="image" src="https://github.com/user-attachments/assets/dbf8480d-ef40-46b4-af00-0e0143934c34" />

## Step 2: What is the first ingredient that Rick needs?
1) While examining the website, I found the username **R1ckRul3s** when I was inspecting the code. Can it be used for ssh? If so we need to find the password first. Let's check if **robots.txt** is available in the attempts to find the password. I'm going to use curl to do so.

<img width="1213" height="360" alt="image" src="https://github.com/user-attachments/assets/9c43c088-c371-4544-8d73-e00c4fe984fc" />

Found the password **Wubbalubbadubdub** <br>
Now let's try the username and password to access ssh. But when I tried doing so, I got permission denied. So, clearly it is not used for this. So, maybe there might be a login page to use the credentials. <br>

2) While deep inspecting the source code, I found out that there is an assets folder and giving the path to the URL as 10.48.145.44/assets gave me a list of files under assets.

<img width="1919" height="871" alt="image" src="https://github.com/user-attachments/assets/d1905080-b51e-476d-b6cd-30ee4f9620fa" />

<img width="1919" height="864" alt="image" src="https://github.com/user-attachments/assets/5e86bc04-c669-421b-8ebd-7795f4e37e28" />

Upon inspecting each file, nothing was relevant enough to get the login page. 

3) So, I'm going to use gobuster to see if I can find any relavant pages.

<img width="1370" height="746" alt="image" src="https://github.com/user-attachments/assets/5e12911c-f330-4a2e-a7f1-19a58e819e39" />

<img width="1420" height="323" alt="image" src="https://github.com/user-attachments/assets/aa152210-59a2-4137-8b47-49c5b4ef3cfa" />

And here, I found login.php and portal.php file and both lead to the login page. Let's use the credential we got to login to the page.

<img width="1919" height="859" alt="image" src="https://github.com/user-attachments/assets/bb289f30-7318-4d50-861a-b26b55b90591" />

4) Upon logging in to the portal, we got a command panel.

<img width="1919" height="470" alt="image" src="https://github.com/user-attachments/assets/1ad7dcaa-8c7f-4095-9570-415436d52308" />

I'm going to try ls to list the files in the panel.

<img width="1919" height="697" alt="image" src="https://github.com/user-attachments/assets/e78340b3-6f90-4376-9c78-3174b2269fec" />

Looks like we got our file for our first ingredient. But, when I tried **cat** to read the contents of the file the command is not available. So, next I tried to use less to see if contents are displayed and yes we got the answer.

<img width="1807" height="473" alt="image" src="https://github.com/user-attachments/assets/fde75b54-0bd8-4f81-a4c6-b31b36f1b480" />

We can also directly type the file name in the URL path to view the content, if in case it allows.

<img width="946" height="291" alt="image" src="https://github.com/user-attachments/assets/f151ed7d-8e25-4415-a3ef-ead065890f02" />

So, the first answer to the quention is **mr.meeseek hair**

## Step 3: What is the second ingredient in Rick’s potion?
1) Now to find the second ingredient, we have got a clue.txt file to view. It tells us to go through the file system. Since the command panel acts as a Linux machine let's try.

```bash
ls /home
```

<img width="1535" height="410" alt="image" src="https://github.com/user-attachments/assets/2d725baf-cab9-4424-a56c-b982c2a9af31" />

2) We got rick and ubuntu. Ubuntu seems normal to me and since this room is about Rick, let's view the contents in rick user and we got something like second ingredients.

<img width="1502" height="336" alt="image" src="https://github.com/user-attachments/assets/8e264321-9b2e-4692-a042-dd57586d9ab9" />

3) Upon using the less command we got the second ingredient to be **1 jerry tear**

```bash
less /home/rick/"second ingredients"
```

<img width="1279" height="413" alt="image" src="https://github.com/user-attachments/assets/f43fd764-5160-49fa-9866-deb27d2accbd" />

## Step 4: What is the last and final ingredient?
1) We don't have anymore clues to get the third ingredient. Maybe this means we need to do privilege escalation to find more on the system. But upon using some commands I came upon the idea to use sudo directly and see and surprisingly the command line allows us to do sudo without any password. So, let's use sudo to list the files in root user.

```bash
sudo ls /root
```

<img width="1234" height="356" alt="image" src="https://github.com/user-attachments/assets/9a37f024-4b42-464d-bf38-1dd58b2e1950" />

2) Now, we have got a file 3rd.txt, Upon viewing it we got the ingredient to be **fleeb juice**

```bash
sudo less /root/3rd.txt
```

<img width="1267" height="418" alt="image" src="https://github.com/user-attachments/assets/b8c3abf6-5ef0-4623-8d07-9e1935c64b9f" />

### Conclusion 
Through this CTF, I have learned to be practical with Linux file system navigation and also learned how to systematically hunt for hidden clues accross different user directories. I also gained firsthand experience with basic privilege escalation, discovering how misconfigured permissions like a passwordless sudo command can grant full root access. Ultimately, this room highlighted the critical importance of secure system configurations and demonstrated how attackers combine simple information disclosure bugs together to achieve full system compromise.





