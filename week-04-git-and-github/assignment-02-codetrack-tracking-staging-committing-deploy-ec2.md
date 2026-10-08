# Assignment 2 — CodeTrack: Tracking, Staging, Committing + Deploy to EC2

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will track and stage project files, create two meaningful Git commits in `CodeTrack`, verify your commit history, and deploy the CodeTrack static website to an EC2 instance using Nginx. This connects local version-control practice with a basic manual deployment workflow used in real DevOps environments.

---

# Task 1 — Verify Git Setup and Enter the Repository

## Goal

Confirm that Git works and that you are inside the correct `CodeTrack` repository.

### Evidence

#### Screenshot 1 — Output of `pwd` showing you're inside `CodeTrack`

<img width="341" height="68" alt="image" src="https://github.com/user-attachments/assets/2582146c-ae97-4a72-8a0f-a78d8c9d0bcc" />


---

#### Screenshot 2 — Output of `git status` showing no "not a git repository" error

<img width="382" height="155" alt="image" src="https://github.com/user-attachments/assets/e2f14375-1039-4587-981a-a3dab17d3708" />


---

# Task 2 — Create index.html and style.css

## Goal

Create the two starter UI files inside `CodeTrack`.

### Evidence

#### Screenshot 3 — Output of `ls` showing `index.html` and `style.css`

<img width="277" height="89" alt="image" src="https://github.com/user-attachments/assets/1954f3d3-88b3-4190-8dce-4473436910fe" />


---

# Task 3 — Add Starter Content

## Goal

Copy the provided starter HTML and CSS content into your local `index.html` and `style.css` files.

### Evidence

#### Screenshot 4 — Your editor showing the contents of `index.html` and `style.css`

<img width="1920" height="1080" alt="Screenshot (185)" src="https://github.com/user-attachments/assets/b4593f11-56f1-40df-958d-f9a767756afc" />


---

# Task 4 — Track and Stage Files Correctly

## Goal

Confirm both files show as untracked, then stage them individually with `git add`.

### Evidence

#### Screenshot 5 — Output of `git status` showing both files as untracked

<img width="1886" height="314" alt="Screenshot (186)" src="https://github.com/user-attachments/assets/cd78eb3f-e8d1-42eb-9100-c3439002ba24" />


---

#### Screenshot 6 — Output of `git status` showing both files staged under "Changes to be committed"

<img width="1869" height="362" alt="Screenshot (187)" src="https://github.com/user-attachments/assets/cbbc714f-1fec-450e-9810-0ad73383950d" />


---

# Task 5 — Create the First Commit (Clean Initial Commit)

## Goal

Commit the staged starter files using the message `Initial UI scaffold: add index.html and style.css`, then check the log.

### Evidence

#### Screenshot 7 — Output of `git commit`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/512ee829-a202-44b4-91e2-40eb87e0e93a" />


---

#### Screenshot 8 — Output of `git log --oneline` showing the first commit

<img width="1920" height="1080" alt="Screenshot (190)" src="https://github.com/user-attachments/assets/4b179639-029c-4d5f-81e3-8685f1e639a5" />


---

# Task 6 — Modify index.html and Create a Second Commit

## Goal

Follow the instruction comment inside `index.html` to update the Student Name and Group Name, then commit that change separately using the message `Update homepage content: heading, tagline, CTA button`.

### Evidence

#### Screenshot 9 — Browser showing the updated page with your Student Name and Group Name visible

<img width="437" height="291" alt="image" src="https://github.com/user-attachments/assets/d82aab34-74bc-44ba-8b3f-4e62d0c9fbfd" />


---

#### Screenshot 10 — Output of `git status` showing `index.html` as modified

<img width="352" height="110" alt="image" src="https://github.com/user-attachments/assets/49dbf7ca-acc3-468e-abbc-1b9fe78804ab" />


---

#### Screenshot 11 — Output of `git commit`

<img width="442" height="113" alt="image" src="https://github.com/user-attachments/assets/b9162827-6d20-489b-b993-64b9aa72b4a2" />


---

#### Screenshot 12 — Output of `git log --oneline` showing two commits

<img width="321" height="75" alt="image" src="https://github.com/user-attachments/assets/01bde188-e624-477e-bc7a-bfeb7d5fb3fb" />


---

# Task 7 — Deploy to EC2 with Nginx (Static Website)

## Goal

Install and start Nginx on your EC2 instance, then copy `index.html` and `style.css` into the Nginx web root.

### Evidence

#### Screenshot 13 — Output of `systemctl status nginx --no-pager` showing Nginx `active (running)`

<img width="1920" height="561" alt="Screenshot (191)" src="https://github.com/user-attachments/assets/9484f31d-6e71-41a3-8407-bb7dbcd6e2fd" />


---

#### Screenshot 14 — Output of `curl -I http://localhost` showing `HTTP/1.1 200 OK`

<img width="1920" height="472" alt="Screenshot (192)" src="https://github.com/user-attachments/assets/e3084e0a-daf0-4367-8580-03ae76e8abc8" />


---

#### Screenshot 15 — Browser showing the CodeTrack site loaded at `http://<EC2_PUBLIC_IP>`, with your Full Name and Group Name visible

<img width="439" height="289" alt="image" src="https://github.com/user-attachments/assets/b711e0f3-3e71-471c-855a-82f56751dfc6" />


---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://lnkd.in/p/eqamUZVY

---

#### Screenshot — LinkedIn post showing the deployed CodeTrack application

<img width="1920" height="1080" alt="Screenshot (193)" src="https://github.com/user-attachments/assets/1512fa66-a441-47dc-92b9-5956d69bb5a9" />


---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name and Group Name must be visible in the deployed application evidence
- `git log --oneline` output must show at least two meaningful commits
- Do not expose AWS access keys, passwords, private key contents, or other sensitive information

---

# Completion Checklist

- [ ] `CodeTrack` repository verified with `git status` (Screenshots 1–2)
- [ ] `index.html` and `style.css` created and populated (Screenshots 3–4)
- [ ] Starter files staged and committed in the first commit (Screenshots 5–8)
- [ ] Student Name and Group Name updated in `index.html` (Screenshot 9)
- [ ] Second controlled commit created (Screenshots 10–12)
- [ ] Nginx active on the EC2 instance and CodeTrack reachable via its public IP (Screenshots 13–15)
- [ ] LinkedIn post published and URL submitted
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
