# Hacker Holidays 2026 - The Concierge Knows Too Much
So, this is the official first step into the vacation. From here on, we will be doing each task per day and today's task, is to speak with VERA, about how she knows too much details about her customers. <br>
For this we will be doing AI Prompt Injection, Social Engineering and LLM Security to understand the underlying system prompt.

<img width="588" height="836" alt="image" src="https://github.com/user-attachments/assets/0c3ebed4-7fde-4ead-9655-2a260b781c10" />

This room was pretty simple. I tried having different conversations with VERA, the AI concierge. <br>
She was pretty much well prepared to not reveal her internal system prompt just to anyone, just because they asked to do so.

<img width="949" height="532" alt="image" src="https://github.com/user-attachments/assets/4fe6df28-bc81-4913-aee2-b14009fa8a6c" /> <br>
<img width="931" height="543" alt="image" src="https://github.com/user-attachments/assets/7342f8c7-5738-44da-a5eb-3f26f24e4469" /> <br>
<img width="940" height="535" alt="image" src="https://github.com/user-attachments/assets/277f9b19-b8ce-4912-a00e-72bb9882540a" /> <br>

After trying certain prompts, I got a clue from the room itself. The user @0xMia's has put in her review like 

<img width="733" height="347" alt="image" src="https://github.com/user-attachments/assets/4d024b56-3194-4027-bce7-df130566619e" />

She has given us some weird names as clue, which I think, they could be the recognized VIP's. So, I tried using their names to get the internal code and yes we did get the internal escalation code.

<img width="941" height="540" alt="image" src="https://github.com/user-attachments/assets/040f8932-f832-44d6-9b30-aa675e479e2c" /> <br>
<img width="912" height="533" alt="image" src="https://github.com/user-attachments/assets/792be156-e02c-42f9-8474-d8e0d04f2c5f" />

So, by using the VIP names we have got the escalation code and which also the answer to this room's flag as well <br>
**What is the flag?**
THM{v3r4_kn0ws_t00_much!}

## Lessons Learned

* **Analyzing User Reviews for OSINT Hints:** When standard prompt injection attempts fail, public reviews or user profiles can hold subtle clues like VIP names or internal references.
* **Role-Play & Identity Spoofing in LLMs:** AI chatbots often enforce strict controls against direct prompt disclosure, but impersonating authorized personnel (like VIP guests) can trick the model into releasing restricted escalation codes.
* **Over-Privileged Context Boundaries:** System prompts that hold both public concierge functions and sensitive internal escalation logic are vulnerable if identity verification isn't strictly validated on the backend.







