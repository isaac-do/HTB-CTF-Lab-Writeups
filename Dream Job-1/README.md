# Challenge Context
- **Name**: Dream Job-1
- **Difficulty**: Very Easy
- **Category**: Threat Intelligence
- **OS**: Windows
- **CTF Date**: 03-06-2025
- **Description**: 
> You are a junior threat intelligence analyst at a Cybersecurity firm. You have been tasked with investigating a Cyber espionage campaign known as Operation Dream Job. The goal is to gather crucial information about this operation.

# Writeup
## Task 1
### Who conducted Operation Dream Job?
<img width="1570" height="612" alt="image" src="https://github.com/user-attachments/assets/eec11053-bb56-41f0-9a0a-d4683e5d7f9c" />
<img width="176" height="172" alt="image" src="https://github.com/user-attachments/assets/2a31c18d-03b3-48ab-a41b-bc18f8e1eabb" />
<img width="1342" height="644" alt="image" src="https://github.com/user-attachments/assets/8e3e548a-b6d9-4e82-b6b1-4093aa93b63f" />

First, I visited the MITRE ATT&CK page, which is used for threat intelligence. Then I navigated to "CTI", then under CTI to "Campaign". Under the "Campaigns" side menu, I scrolled down until I found Operation Dream Job.
The first sentence stated who conducted Operation Dream Job.

### Final Answer
Lazarus Group

## Task 2
### When was this operation first observed?
<img width="1391" height="358" alt="image" src="https://github.com/user-attachments/assets/d06e7aeb-a6c7-4155-ac0d-74168ddfb7b3" />

### Final Answer
September 2019

## Task 3
### There are 2 campaigns associated with Operation Dream Job. One is Operation North Star, what is the other?
<img width="1398" height="612" alt="image" src="https://github.com/user-attachments/assets/da81b4e9-3abc-45ba-b107-14c00ccc390a" />

### Final Answer
Operation Interception

## Task 4
### During Operation Dream Job, there were the two system binaries used for proxy execution. One was Regsvr32, what was the other?
<img width="1383" height="146" alt="image" src="https://github.com/user-attachments/assets/2466d320-716f-4b07-805b-ec33ea9c6ad4" />

I used Ctrl-F to find "Proxy execution" and found the second technique used.

### Final Answer
Rundll32

## Task 5
### What lateral movement technique did the adversary use?
<img width="1414" height="722" alt="image" src="https://github.com/user-attachments/assets/937a1785-6108-4e7e-aace-2a259ed3ef84" />
<img width="128" height="221" alt="image" src="https://github.com/user-attachments/assets/09e626ec-23f6-404f-87cc-5ce81e96bad7" />

I navigated to the ATT&CK Navigator Layers, then scrolled to the right to find "Lateral movement".

### Final Answer
Internal Spearphishing

## Task 6
### What is the technique ID for the previous answer?
<img width="391" height="294" alt="image" src="https://github.com/user-attachments/assets/7dc102f2-896a-4278-be72-465137cb4c58" />

Hovering over Internal Sphishing reveals the technique ID.

### Final Answer
T1534

## Task 7
### What Remote Access Trojan did the Lazarus Group use in Operation Dream Job?
<img width="1373" height="298" alt="image" src="https://github.com/user-attachments/assets/c6594137-c174-4fd4-95a5-bcabd572a233" />
<img width="1393" height="426" alt="image" src="https://github.com/user-attachments/assets/62a57c2c-8f0d-428c-9fce-5e3f44691659" />

### Final Answer
DRATzarus

## Task 8
### What technique did the malware use for execution?
<img width="1389" height="388" alt="image" src="https://github.com/user-attachments/assets/d46dec8f-e770-4795-b1f5-a1b25d370daf" />
<img width="137" height="651" alt="image" src="https://github.com/user-attachments/assets/2ca6f7a4-6e7e-4715-9d45-89e567e4809d" />

### Final Answer
Native API

## Task 9
### What technique did the malware use to avoid detection in a sandbox?
<img width="1406" height="783" alt="image" src="https://github.com/user-attachments/assets/3eec3c84-11b0-4235-8b2f-ea59874e00cf" />

### Final Answer
Time Based Evasion

## Task 10
### To answer the remaining questions, utilize VirusTotal and refer to the IOCs.txt file. What is the name associated with the first hash provided in the IOC file?
<img width="1605" height="476" alt="image" src="https://github.com/user-attachments/assets/ec9e0f22-c191-4bae-8024-ab74d484e23a" />

### Final Answer
IEXPLORE.exe

## Task 11
### When was the file associated with the second hash in the IOC first created?
<img width="1611" height="911" alt="image" src="https://github.com/user-attachments/assets/6ae11b21-262d-4b33-9ef0-a4b24240478f" />

### Final Answer
2020-05-12 19:26:17

## Task 12
### What is the name of the parent execution file associated with the second hash in the IOC?
<img width="1150" height="923" alt="image" src="https://github.com/user-attachments/assets/ffb74da9-8d7b-49e4-8cfc-aeb79236964a" />

### Final Answer
BAE_HPC_SE.iso

## Task 13
### Examine the third hash provided. What is the file name likely used in the campaign that aligns with the adversary's known tactics?
<img width="1589" height="933" alt="image" src="https://github.com/user-attachments/assets/29b7324e-a178-4074-a02e-80c4337c793c" />

### Final Answer
Salary_Lockheed_Martin_job_opportunities_confidential.doc

## Task 14
### Which URL was contacted on 2022-08-03 by the file associated with the third hash in the IOC file?
<img width="1445" height="766" alt="image" src="https://github.com/user-attachments/assets/52e7571d-3ea5-4b8e-8e21-80893fed00e7" />

### Final Answer
https://markettrendingcenter.com/lk_job_oppor.docx
