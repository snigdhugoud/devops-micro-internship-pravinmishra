# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`


<img width="842" height="345" alt="Screenshot 2026-10-07 083025" src="https://github.com/user-attachments/assets/6cbd6cd3-d47e-4711-87bd-1467b523e674" />


---

#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2e35fce8-9027-4cd5-8127-195f66be2d76" />


---

### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**

The systemctl status nginx --no-pager command shows that Nginx is active (running). This confirms that the Nginx service is currently working.

---

**2. What proves that the server is listening for HTTP traffic?**

The ss -tlnp command shows Nginx listening on port 80, which is the standard port for HTTP traffic. This proves the server is ready to receive web requests.

---

**3. Why must you capture a healthy baseline before simulating an incident?**

A healthy baseline shows how the server works when everything is normal. After simulating an incident, we can compare the new results with the baseline to clearly identify what changed and confirm that the problem was caused by the incident.

---

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)


<img width="1920" height="1080" alt="Screenshot (163)" src="https://github.com/user-attachments/assets/93bc6859-a0e9-45a7-8f6a-616cfc70ac8e" />

---

### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

Project-specific rules tell Claude how the project should be handled safely and consistently. They help Claude follow the correct workflow, understand the project structure, and avoid unsafe actions.

---

**2. Why is the human required to execute the recovery command?**

The human must execute the recovery command so that an important system change is not made automatically by Claude. This keeps the recovery process under human control and reduces the risk of causing further problems.

---

**3. Which rule prevents Claude from making an unsupported diagnosis?**

The Safety Rules prevent unsupported diagnosis by requiring Claude to use actual evidence, such as command output and logs, before identifying the cause of an incident.

---

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results


<img width="1920" height="1080" alt="Screenshot (164)" src="https://github.com/user-attachments/assets/6d174b7e-0a07-4391-9f51-e588d01eef9e" />


---

### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

The read-only inspection is the Gather phase. Claude collected information about the Nginx service, port 80, HTTP response, configuration, and error logs before taking any action.

---

**2. Did Claude follow the instruction not to create files? How did you verify this?**

Yes. Claude followed the instruction and only performed read-only checks. I verified this by reviewing the commands it executed and confirming that no file-creation or modification commands were used.

---

**3. Why is planning before coding useful in DevOps automation?**

Planning helps identify the required steps before making changes. It reduces mistakes, makes the workflow safer and more organized, and helps ensure that automation performs only the intended actions.

---

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array


<img width="1920" height="1080" alt="Screenshot (165)" src="https://github.com/user-attachments/assets/b193ee93-b5d6-4932-9c0f-eed12508eb8d" />

---

#### Screenshot 6 — Middle section showing check functions and conditionals


<img width="1920" height="1080" alt="Screenshot (166)" src="https://github.com/user-attachments/assets/fde23a89-9f68-4e87-b75c-ae192df1102b" />


---

#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior


<img width="1920" height="1080" alt="Screenshot (167)" src="https://github.com/user-attachments/assets/f8ae1a84-a212-49ad-932c-ff9e8cd91438" />


---

#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission


<img width="1920" height="1080" alt="Screenshot (168)" src="https://github.com/user-attachments/assets/dba88d28-94d6-42f4-9b17-de52843f9094" />


---

### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The checks array stores the names of the different health checks that the script needs to perform, such as Nginx status, port status, HTTP response, disk usage, memory usage, and error logs.

---

**2. How does the `for` loop use that array?**

The for loop goes through each item in the checks array one by one and runs the corresponding health-check logic.

---

**3. Why are the health checks separated into functions?**

Functions keep each health check organized and easier to understand. They also make the script easier to maintain, test, and reuse.

---

**4. What is the purpose of `$(...)` in this script?**

$(...) is command substitution. It runs a command and puts its output into the script so that the result can be stored in a variable or used in another command.

---

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

Different exit codes allow the script to clearly communicate the health condition. HEALTHY means everything is normal, WARN means there may be a concern, and FAIL means a serious problem was detected. This makes the results easier for people and automation tools to interpret.

---

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results


<img width="1920" height="1080" alt="Screenshot (169)" src="https://github.com/user-attachments/assets/5a997206-731a-4620-a652-639258443762" />


---

#### Screenshot 10 — Output showing the captured exit code and final summary


<img width="1920" height="1080" alt="Screenshot (170)" src="https://github.com/user-attachments/assets/4ac00415-cbe1-4d56-b29f-7919d9acadf7" />


---

### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**
The overall status of my healthy baseline is HEALTHY because the Nginx service is running, the HTTP port is listening, and the application is responding normally.

---

**2. Which exact Linux evidence proves the application is serving traffic?**

The curl -I http://localhost command proves that the application is serving traffic because it returns an HTTP response from the Nginx server.

---

**3. Did your script return exit code 0 or 1? Explain why.**

The script returned exit code 0 because all required health checks passed and the system was in a healthy state.

---

**4. What is the difference between a warning and a failure in this script?**

A warning means a condition has crossed a caution threshold but the service can still be working normally. A failure means an important health check has failed and the application or service may not be working correctly.

---

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules


<img width="1920" height="1080" alt="Screenshot (171)" src="https://github.com/user-attachments/assets/ebfdb490-eae5-41e3-a496-2dca444521f2" />


---

#### Screenshot 12 — `/linux-triage` output for the healthy server

<img width="1920" height="1080" alt="Screenshot (172)" src="https://github.com/user-attachments/assets/20db3b6f-967a-49d9-bc75-d4575706d42c" />


---

### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

The skill needs Bash to run Linux commands, Read to inspect files, and Grep to search for specific information. It does not need Write because the purpose of the skill is to check and diagnose the server, not to modify files.

---

**2. Why is `disable-model-invocation: true` useful for this skill?**

disable-model-invocation: true means Claude will not automatically run this skill on its own. It must be triggered manually by the user. This gives the user more control over when the server health-check is performed.

---

**3. What part is performed by Bash, and what part is performed by Claude?**

Bash performs the actual Linux commands and collects evidence from the server. Claude reads and analyzes that evidence and explains whether the server appears healthy or if there are problems

---

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

It is better because Claude makes its conclusion using real server evidence instead of guessing. The commands provide information such as service status, processes, files, and system conditions, making the health assessment more reliable.

---

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

<img width="1920" height="1080" alt="Screenshot (173)" src="https://github.com/user-attachments/assets/d99f7aa3-21e6-4f43-ab0a-55d8e4a133a6" />


---

#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

Add your screenshot here.

---

#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. Which three checks failed?**

Add your answer here.

---

**2. What evidence supports the conclusion that Nginx is unavailable?**

Add your answer here.

---

**3. Did Claude execute the recovery command? Why is that important?**

Add your answer here.

---

**4. Which phase of the Agentic Loop is represented by the Bash report?**

Add your answer here.

---

**5. Which phase is represented by Claude's explanation?**

Add your answer here.

---

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

Add your screenshot here.

---

#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

Add your screenshot here.

---

#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

Add your screenshot here.

---

#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

Add your answer here.

---

**2. What evidence proves that the service recovered?**

Add your answer here.

---

**3. Why is the second triage run necessary?**

Add your answer here.

---

**4. What could go wrong if an AI agent automatically restarted every failed service?**

Add your answer here.

---

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**

Add your answer here.

---

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** Add your full name here

**Date:** DD/MM/YYYY

---

**1. Reported Symptom**

Add your answer here.

---

**2. Evidence Collected**

Add your answer here.

---

**3. Most Likely Cause**

Add your answer here.

---

**4. Human-Approved Recovery Action**

Add your answer here.

---

**5. Verification**

Add your answer here.

---

**6. Safety Decision**

Add your answer here.

---

**7. Agentic Loop Mapping**

Add your answer here.

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

# GitHub Repository URL

Paste the URL of your GitHub folder or repository containing the assignment files here:

`Add your URL here`

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- [ ] Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- [ ] Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- [ ] Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- [ ] Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- [ ] Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- [ ] Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- [ ] Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- [ ] Incident summary contains all seven required sections
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots and the Bash report
- [ ] Skill does not have Write permission
- [ ] Skill did not execute any recovery commands
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
