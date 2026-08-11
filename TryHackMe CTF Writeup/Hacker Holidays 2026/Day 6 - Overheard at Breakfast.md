# Hacker Holiday's 2026 - Overheard at Breakfast
The **Overheard at Breakfast** challenge takes place on the breakfast terrace of the Byte Lotus Hotel, where a guest managed to capture a screenshot of an exposed conversation during a brief moment of inattention. 

In this OSINT challenge, the objective is to analyze the conversation snippets, extract subtle identifying clues, and follow the digital breadcrumbs across social platforms to locate a hidden account and retrieve the flag.

This is what the concierge has let us know in the beginning of this room and a user has also posted in their Social Media about this.

<img width="1042" height="431" alt="image" src="https://github.com/user-attachments/assets/dd09c830-2388-4d79-a9c5-7c88ed7b03c2" />

<img width="443" height="297" alt="image" src="https://github.com/user-attachments/assets/0a52b32e-719a-4c01-b843-b97933fbc62c" />

They have given us an image about the conversation that has happened in the table. The clue they have left in the table.

<img width="1175" height="781" alt="conversation" src="https://github.com/user-attachments/assets/fa63bc60-f8be-420e-8283-1507107c6194" />

We see here that VIP Guest Lambo has shared his email for communication in this conversation **lambobytelotushotel@gmail.com**. Another hint what we see here is that, Lambo here says he used to have a free tool which he used for handling social media accounts but later he wiped out all details and now he remembers the tool started with "G". If we remember correctly, in OSINT we have a tool which aligns with these specifications called **Gravatar**.

**Gravatar** known as **Globally Recognized Avatar**, is a powerful OSINT tool. It converts a target email address into an MD5 or SHA256 hash, investigators can query public endpoints to discover associated profile pictures, display names, biographies, social media links, and previously used user names.

So, if we want to find Lambo's Gravatar account, all we have to do is to hash Lambo's email ID. So, for that, I'm going to use the terminal from the AttackBox provided by TryHackMe. We need to first convert this email ID to a hash so I'll use the command ```echo -n "lambobytelotushotel@gmail.com" | md5sum```. Here, the -n flag is used to tell echo to not add any extra white line in the end. If **-n** is not given then MD5 will perform hash for the white new line as well.

<img width="933" height="207" alt="image" src="https://github.com/user-attachments/assets/2f7935b3-9280-448e-ac92-458d39cb2694" />

Now using the hashed email ID, we will now go to the browser directly and access the gravatar account using the url **https://gravatar.com//d4a5fc5d3128890778667e24617d7cc0** and we got Lambo's Profile.

<img width="858" height="594" alt="image" src="https://github.com/user-attachments/assets/c36c2444-78f5-47cd-8c3f-02631c15a468" />

This account tells us that we have come to right place on the internet and as for a prize they have given us an encoded string, which looks like Base64 encoded using ASCII. So, let's decode it using **Cyberchef** or we can also use the terminal's built-in Base64 operation.

<img width="1919" height="709" alt="image" src="https://github.com/user-attachments/assets/595b14a7-9217-4c4c-935c-f6f398aa2d24" />

Using Cyberchef, I have retrieved the flag.

I'll also demonstrate the terminal way as well. I have used the command ```echo "VEhNe1MzY3JlVF9QcjBmaWwzX0g0c19iMzNuX0lkZW50MWZpM2R9" | base64 -d```

<img width="938" height="242" alt="image" src="https://github.com/user-attachments/assets/c817fa8c-757e-4bd0-a087-b8dd3fa49ae7" />

**What is the flag?** <br>
THM{S3creT_Pr0fil3_H4s_b33n_Ident1fi3d}

## Lessons Learned

* **Social Media & Public Email OSINT Exposure:** Email addresses shared in casual conversations or public forums can be cross-referenced across online services (such as Gravatar) to reveal hidden user profiles, display names, and personal data.
* **Hash Enumeration Risks:** Common email hashing standards (like MD5 or SHA256) used by avatar and profile distribution platforms can be easily replicated or reversed once the plain-text email is known, leading to profile discovery.
* **Avoid Storing Sensitive Strings in Public Bio Fields:** Storing encoded flags, secret keys, or sensitive text strings in publicly accessible profile bios or custom fields enables trivial extraction once the profile endpoint is discovered.
* **Sanitize String Input Before Hashing:** Command-line operations require explicit flags (e.g., `echo -n`) to prevent unexpected newline characters (`\n`) from altering the resulting hash output and breaking verification.









