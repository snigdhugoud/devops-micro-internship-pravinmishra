# Assignment 4 — Building Your AI Team

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build and configure a set of specialized AI subagents inside your project. You will learn how different models and tool permissions define agent behavior, and you will trigger two real agent delegations to analyze security and cost aspects of your Terraform infrastructure.

---

# Task 1 — Create the Agents Folder and Add Files

## Goal

Create the `.claude/agents/` directory and add all required agent files.

### Evidence

#### Screenshot 1 — VS Code sidebar showing `.claude/agents/` with all 3 files

<img width="1920" height="1080" alt="Screenshot (49)" src="https://github.com/user-attachments/assets/a42bec11-201e-41fb-9f52-3f6ecd571c68" />


---

# Task 2 — Compare the Agent Configurations

## Goal

Analyze the configuration differences between the three agents and demonstrate understanding of model and tool selection.

### Written Answers

#### 1. Why does the cost optimizer use Haiku instead of Sonnet?

The cost optimizer uses Haiku instead of Sonnet because cost optimization focuses mainly on analyzing resource usage, identifying unnecessary expenses, and suggesting simple improvements. Haiku is faster and less expensive while still being capable of handling these tasks. Using Haiku helps reduce AI usage costs without needing the more advanced reasoning capabilities of Sonnet for routine cost-analysis work.

---

#### 2. Why does the security auditor NOT have Write in its tools list?

The security auditor does not have the Write tool because it is designed to inspect and analyze files for security issues, not modify them. Keeping it read-only prevents accidental changes to the project and makes the security audit safer and more controlled

---

#### 3. Why does the tf-writer use `inherit` instead of a specific model?

The tf-writer uses inherit so it follows the model selected in the main Claude Code session. This gives the agent flexibility and avoids requiring a specific model, allowing the appropriate model to be used for the Terraform task.

---

### Evidence

#### Screenshot 2 — `security-auditor.md` frontmatter showing model and tools configuration

<img width="1920" height="1080" alt="Screenshot (50)" src="https://github.com/user-attachments/assets/8c7263b1-c858-403b-ac74-95eab368f8af" />


---

#### Screenshot 3 — `cost-optimizer.md` frontmatter showing the model and tools configuration

<img width="1920" height="1080" alt="Screenshot (51)" src="https://github.com/user-attachments/assets/edbe29d7-6f08-4f56-b64a-7e1c4020020c" />


---

# Task 3 — Run the Security Auditor

## Goal

Trigger the security auditor agent and analyze the generated security report for your Terraform infrastructure.

### Evidence

#### Screenshot 4 — The delegation message showing Claude launched the security-auditor


<img width="1257" height="1023" alt="Screenshot (56)" src="https://github.com/user-attachments/assets/732a9f9d-ac8e-4a60-b9e4-44b8d8ada771" />


---

#### Screenshot 5 — Security audit report output


<img width="1280" height="996" alt="Screenshot (57)" src="https://github.com/user-attachments/assets/4f58883d-ec14-4476-8d13-b4eed51ebd04" />


---

# Task 4 — Run the Cost Optimizer

## Goal

Trigger the cost optimizer agent and review the generated cost optimization report.

### Evidence

#### Screenshot 6 — The full cost optimization report


<img width="1263" height="1030" alt="Screenshot (58)" src="https://github.com/user-attachments/assets/caddd2ff-8c0a-4beb-83a4-d02b156185f9" />


---

# Submission Instructions

- Ensure all agent files are committed in `.claude/agents/`
- Complete all written answers in your GitHub Repo
- Push final changes to your forked GitHub repository

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/snigdhugoud/devops-micro-internship-pravinmishra

---

# Completion Checklist

- [ ] `.claude/agents/` folder contains all 3 agent files
- [ ] Screenshot 2 shows correct `security-auditor.md` configuration
- [ ] Screenshot 3 shows correct `cost-optimizer.md` configuration
- [ ] All 3 written answers completed 
- [ ] Security auditor executed successfully
- [ ] Cost optimizer executed successfully
- [ ] Security report is visible with findings
- [ ] Cost report is visible with recommendations
- [ ] All required screenshots added
- [ ] GitHub repo updated with agents

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
