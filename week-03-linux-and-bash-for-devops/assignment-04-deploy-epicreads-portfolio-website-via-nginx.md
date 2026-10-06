# Assignment 4 — Deploy EpicReads Portfolio Website via Nginx

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will deploy a static portfolio website on an Ubuntu VM using Nginx. You will download the website template, add your ownership proof in the footer, deploy the files to the Nginx web root, and verify the website is publicly accessible via a browser.

---

# Task 0 — Pre-flight Check

## Goal

Verify the Ubuntu VM and Nginx are ready for deployment.

### Evidence

#### Screenshot 0 — Output of `sudo systemctl status nginx --no-pager` showing Active (running)

<img width="1776" height="683" alt="Screenshot (129)" src="https://github.com/user-attachments/assets/ce9b2373-6c19-4132-902a-36519d647926" />


---

# Task 1 — Get the Website Source Code

## Goal

Download and extract the portfolio website template.

### Evidence

#### Screenshot 1 — Output of `ls -la` showing the extracted project folder

<img width="1920" height="1080" alt="Screenshot (128)" src="https://github.com/user-attachments/assets/3a4add74-18e9-4014-9751-7eb57ed19faf" />


---

# Task 2 — Add Ownership Proof (Anti-Copy Change)

## Goal

Update the website footer with your deployment details.

### Evidence

#### Screenshot 2 — Nano editor open with the updated footer showing your Full Name, Group, Week, and Date



<img width="1920" height="1080" alt="Screenshot (134)" src="https://github.com/user-attachments/assets/302ab1ba-a46a-4895-ae90-4f338ac43f75" />


---

# Task 3 — Deploy Website via Nginx

## Goal

Deploy the portfolio website to the Nginx web root.

### Evidence

#### Screenshot 3 — Output of `sudo nginx -t` showing configuration test successful


<img width="1920" height="1080" alt="Screenshot (132)" src="https://github.com/user-attachments/assets/8dc3f2f6-4395-4a43-9914-c6800485f67f" />


---

#### Screenshot 4 — Output of `ls /var/www/html` showing deployed website files

<img width="1178" height="450" alt="Screenshot (135)" src="https://github.com/user-attachments/assets/c41139b4-7608-464c-b354-ee825fc7c770" />


---

# Task 4 — Verify Website is Live

## Goal

Verify the deployed website is publicly accessible and the footer contains your details.

### Evidence

#### Screenshot 5 — Output of `curl ifconfig.me` showing the server's public IP address

<img width="1858" height="367" alt="Screenshot (136)" src="https://github.com/user-attachments/assets/d821aa8d-cd7d-4d05-9942-2e789c6cb64f" />


---

#### Screenshot 6 — Browser showing the live website with your Full Name and deployment details in the footer

Add your screenshot here.

---

# Task 5 — Mini Real DevOps Operational Check

## Goal

Verify the deployed website and Nginx service are healthy.

### Evidence

#### Screenshot 7 — Output of `systemctl is-enabled nginx`

Add your screenshot here.

---

#### Screenshot 8 — Output of `curl -I http://localhost` showing 200 OK

Add your screenshot here.

---

# LinkedIn Post (Mandatory)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post showing the live website with your Full Name in the footer

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Ownership proof in the footer is mandatory
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Screenshot 0: Nginx service status (active/running)
- [ ] Screenshot 1: Website files downloaded and extracted
- [ ] Screenshot 2: Footer updated with Full Name, Group, Week, and Date
- [ ] Screenshot 3: Nginx configuration test successful
- [ ] Screenshot 4: Website files deployed to /var/www/html
- [ ] Screenshot 5: Public IP retrieved
- [ ] Screenshot 6: Live website accessible in browser with footer details
- [ ] Screenshot 7: Nginx enabled on boot
- [ ] Screenshot 8: Local HTTP response returns 200 OK
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
