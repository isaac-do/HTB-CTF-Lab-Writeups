# Challenge Context
- **Name**: Campfire-2
- **Difficulty**: Very Easy
- **Category**: Forensics
- **OS**: Windows
- **CTF Date**: 06-27-2024
- **Description**:
> Forela's Network is constantly under attack. The security system raised an alert about an old admin account requesting a ticket from KDC on a domain controller. Inventory shows that this user account is not used as of now so you are tasked to take a look at this. This may be an AsREP roasting attack as anyone can request any user's ticket which has preauthentication disabled.
# Writeup
## Task 1
### When did the ASREP Roasting attack occur, and when did the attacker request the Kerberos ticket for the vulnerable user?
<img width="537" height="547" alt="image" src="https://github.com/user-attachments/assets/a7cbc261-d7c9-4fc9-b167-3290d7c8ec21" />
<img width="802" height="908" alt="image" src="https://github.com/user-attachments/assets/a1ffc18c-865f-48a4-832b-9795bbacd28d" />
<img width="783" height="768" alt="image" src="https://github.com/user-attachments/assets/84f92366-d90e-4482-815e-b87b5fb3967c" />

I filtered the event logs to show only events with event ID 4768. Event ID 4768 indicates that a Kerberos authentication ticket was requested. Going through the list of events, I came across an event at 1:36:40 AM (my local time), and I noticed the pre-authentication type is 0, which is an indicator that the pre-authenticator was bypassed.

I then switched to the Details tab and looked under "System" and "TimeCreated" to get the time in UTC.

### Final Answer
2024-05-29 06:36:40https://github.com/isaac-do/HTB-CTF-Lab-Writeups/tree/main

## Task 2
### Please confirm the User Account that was targeted by the attacker.
<img width="812" height="756" alt="image" src="https://github.com/user-attachments/assets/15758e9f-a271-4f33-94ce-f8c2405237b7" />

From the General tab on the same event as Task 1, the Account name logged is arthur.kyle.

### Final Answer
arthur.kyle

## Task 3
### What was the SID of the account?
<img width="802" height="754" alt="image" src="https://github.com/user-attachments/assets/89b479d6-e805-492f-9ce8-a129fd82d037" />

From the General tab on the same event as Task 1, the User ID logged is S-1-5-21-3239415629-1862073780-2394361899-1601.

### Final Answer
S-1-5-21-3239415629-1862073780-2394361899-1601

## Task 4
### It is crucial to identify the compromised user account and the workstation responsible for this attack. Please list the internal IP address of the compromised asset to assist our threat-hunting team.
<img width="797" height="752" alt="image" src="https://github.com/user-attachments/assets/b3769170-3a27-494b-9244-e3c0bbd6d2ee" />

From the General tab on the same event as Task 1, the Client Address logged is 172.17.79.129.

### Final Answer
172.17.79.129

## Task 5
### We do not have any artifacts from the source machine yet. Using the same DC Security logs, can you confirm the user account used to perform the ASREP Roasting attack so we can contain the compromised account/s?
<img width="808" height="749" alt="image" src="https://github.com/user-attachments/assets/8ade89be-8ca5-4c80-b0e0-a7e595bc37f4" />

Looking at the next immediate event that occurred after the pre-authentication bypass, I observe that the IP address is the same one that I identified before.
From this, this is a strong indicator that the user in this log is the compromised account performing the attack.


### Final Answer
happy.grunwald
