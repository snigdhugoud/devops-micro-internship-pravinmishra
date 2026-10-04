# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

Add your screenshot here.

---

#### Screenshot 2 — Output of `ip a`

<img width="1920" height="1080" alt="Screenshot (110)" src="https://github.com/user-attachments/assets/5a24383b-5e5f-42ba-b258-a6f744661b02" />


---

#### Screenshot 3 — Output of `sudo ss -tulpen`

<img width="1920" height="699" alt="Screenshot (111)" src="https://github.com/user-attachments/assets/6fb4bbfc-2a57-4ae4-8c07-ff0a0f98378c" />


---

#### Screenshot 4 — Output of `sudo ufw status`

<img width="1920" height="1080" alt="Screenshot (112)" src="https://github.com/user-attachments/assets/3fbf73e9-3b8f-4ff4-aad6-c66aa1ec029e" />


---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

The output of ss -tulpn shows Nginx listening on 0.0.0.0:80. This means Nginx is accepting HTTP connections on port 80 from all IPv4 network interfaces.

---

**2. What proves SSH is active on port 22?**

The ss -tulpn output shows the SSH service (sshd) listening on port 22. This proves that SSH is active and ready to accept SSH connections.

---

**3. Did you find any unexpected open ports? Explain briefly.**

No unexpected open ports were found. The open ports were related to the required services, such as HTTP on port 80 and SSH on port 22.

---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`


<img width="1920" height="1080" alt="Screenshot (113)" src="https://github.com/user-attachments/assets/b69aeb92-13c4-4b7d-abfd-eef86d3504af" />


---

#### Screenshot 2 — Output of `sudo nginx -t`



<img width="402" height="58" alt="Screenshot 2026-10-04 181331" src="https://github.com/user-attachments/assets/512a45d7-fe7c-456a-a578-05ddc64dbd55" />


---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/24461df4-3e73-47b8-9c68-26a10c6a8573" />


---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart, the website may become unavailable because Nginx cannot serve the application. I would first check the error logs and configuration, fix the problem, and restore the last known working configuration.

---

**2. What's your basic rollback plan?**
My basic rollback plan is to keep a backup of the previous working Nginx configuration. If a new configuration causes problems, I would restore the backup, test it with sudo nginx -t, and restart Nginx after the test succeeds.

---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`


<img width="1845" height="506" alt="Screenshot (115)" src="https://github.com/user-attachments/assets/6805f555-7950-4dbb-ae6b-aedfdf82f8f0" />


---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`


<img width="1790" height="295" alt="Screenshot (116)" src="https://github.com/user-attachments/assets/a5684eab-6abb-484b-94a2-88d7a1b35f4b" />


---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`


<img width="1723" height="230" alt="Screenshot (117)" src="https://github.com/user-attachments/assets/2fabc147-2bd4-41d4-b9e0-9eb391d78823" />


---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

No, there were no recent errors in the Nginx logs during my check. An empty error log or no recent error entries means Nginx did not report any major problems while serving the requests I tested.

---

**2. If there were no errors, what does that indicate about the system?**

It indicates that Nginx is running normally and the server is handling requests without reporting recent errors. This gives confidence that the Nginx configuration and service are working as expected.

---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

Yes, my curl requests were visible in the Nginx access log entries. This proves that the requests reached the Nginx server and that Nginx received and processed the traffic successfully.

---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`


<img width="1854" height="237" alt="Screenshot (118)" src="https://github.com/user-attachments/assets/01e61f99-4d17-4c63-9127-d2465ac96fce" />


---

#### Screenshot 2 — Output of `free -h`


<img width="1804" height="230" alt="Screenshot (119)" src="https://github.com/user-attachments/assets/5495b9d0-4f8d-487e-84e0-e75244d1c8ed" />


---

#### Screenshot 3 — Output of `df -h`


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ce5d45aa-404e-4aea-918d-6895a4345535" />


---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`


<img width="1920" height="423" alt="Screenshot (121)" src="https://github.com/user-attachments/assets/a103b185-1f04-41f7-a8e9-222d33ba27fc" />


---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

Disk usage looks like the most important resource to monitor because a server needs enough free disk space for logs, temporary files, application data, and system operations. If disk usage is already high, it could become a problem sooner than CPU or memory.

---

**2. What happens if disk becomes 100% full in a production server?**

If the disk becomes 100% full, the server may not be able to write new files, logs, temporary data, or application data. This can cause applications and services such as Nginx to fail or behave unexpectedly. Therefore, disk usage should be monitored and cleaned up before it reaches 100%.

---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`


<img width="1920" height="438" alt="Screenshot (122)" src="https://github.com/user-attachments/assets/c61c1853-2613-4e52-a05c-32372b149294" />

---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

<img width="1843" height="296" alt="Screenshot (123)" src="https://github.com/user-attachments/assets/763a087c-7273-43c3-a809-6b7348417440" />


---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

<img width="1805" height="188" alt="Screenshot (124)" src="https://github.com/user-attachments/assets/f075bbff-ca88-4ebe-b252-2cb4d886c966" />


---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

I confirm the correct version by checking the application in the browser and verifying that the expected changes, version number, or deployment message are displayed. I can also check the deployed files and use commands such as grep or ls to verify that the latest files are present.

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

Add your screenshot here.

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

Add your screenshot here.

---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

Write your answer here.

---

**2. How did you fix the issue?**

Write your answer here.

---

**3. How can you avoid this kind of issue in real production systems?**

Write your answer here.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

Add your screenshot here.

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

Write your answer here

---

**2. How did you fix the issue and restore the application?**

Write your answer here.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

Write your answer here.

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

Write your answer here.

---

**2. Why should only required ports be open on a production server?**

Write your answer here.

---

**3. Why is it important for Nginx to be enabled on boot?**

Write your answer here.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

Write your answer here.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Write your answer here.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
