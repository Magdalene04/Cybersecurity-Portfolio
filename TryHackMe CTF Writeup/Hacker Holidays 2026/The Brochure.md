# Hacker Holidays 2026 - The Brochure
TryHackMe's Hacker Holidays challenge is a beginner friendly cybersecurity challenge. Each room is a self-contained hacking challenge: OSINT, web exploitation, cloud security, forensics, AI prompt attacks.

## The Brochure
This room is a little warm up, to the series of hacking challenges we are going to see.

The first thing the room tells us is that this image. This image consists of basic information like getting to know the customer reviews for the hotel and the most loyal Vera, the AI concierge.

<img width="572" height="839" alt="Screenshot 2026-08-07 180015" src="https://github.com/user-attachments/assets/2088a07d-b356-4455-af5b-a611ba06a58a" />

They also have provided a poster about The Byte Lotus hotel where we are to go for the vacation.

<img width="726" height="934" alt="thebrochure" src="https://github.com/user-attachments/assets/0acf39ad-a34d-4abb-bdaf-e47a65a4652a" />

From this poster, we get to know that, Byte Lotus has an official Instagram page, so I did a little bit peaking in their official page and to know that they have very minimal follower rate and following only one single profile which is VERA, the AI Concierge we saw earlier.

According to the first picture we saw, we have several amount of reviews for this staycation, nearly 2500, so why only little amount of followers in this Instagram page? I think it's for us to find later.

<img width="1034" height="1600" alt="blue lotus" src="https://github.com/user-attachments/assets/f659803e-2639-4dc9-b4a1-5f51c5c0cce1" />

So, I went inside the following list and clicked into the VERA profile.

<img width="1080" height="719" alt="vera request" src="https://github.com/user-attachments/assets/63fc4c5c-876f-4f6c-8a03-a5e33fb1f255" />

And inside this account, I found some gibberish posts. Altogether, these gibberish felt like base64 encoded. 

<img width="931" height="1600" alt="VERA" src="https://github.com/user-attachments/assets/db2ee6f5-e687-4fff-91ab-7217982667b4" />

So, the next thing I did is, I went to Cyberchef, a web app for encryption, encoding, compression and data analysis. I gave this base64 encoded details as input to the application and used the conversion method FROM base64. I got the flag from doing this work.

<img width="1919" height="915" alt="image" src="https://github.com/user-attachments/assets/4c349bab-bd12-4319-873a-306a5a2cc265" />

So, now we can answer the question <br>
**What is the flag?** <br>
THM{V3r@s_aCC0unt_h4s_b33n_f0und!}

## Lessons Learned

* **Social Media Footprint Analysis:** Official corporate accounts often link directly to key staff, related sub-accounts, or service bots. Checking the "Following" list is a crucial OSINT step when main profile details are vague.
* **Spotting Profile Anomalies:** A significant mismatch between high engagement (e.g., thousands of reviews) and low follower counts suggests that primary user activity or key evidence is hosted elsewhere.
* **Recognizing Common Data Encodings:** Strings of alphanumeric characters ending with standard padding (like Base64) indicate encoded data rather than random text.
* **Decoding with CyberChef:** Utilizing CyberChef's "From Base64" operation allows for rapid analysis and retrieval of hidden flags or credentials.









