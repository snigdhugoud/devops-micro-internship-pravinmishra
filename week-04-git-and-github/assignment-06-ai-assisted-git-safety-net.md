# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

<img width="1920" height="405" alt="Screenshot (214)" src="https://github.com/user-attachments/assets/1730e17a-e69b-4a93-9a6d-727e898de434" />


---

### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

A dedicated branch allows me to work on a new task without affecting the main branch. It keeps my changes separate, makes it easier to test and review them, and helps prevent mistakes in the main project. Once the changes are ready, I can create a Pull Request to merge them into main.

---

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

<img width="1861" height="342" alt="Screenshot (215)" src="https://github.com/user-attachments/assets/3240e106-e8b3-4e83-a051-f6dcc45ccc54" />


---

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

This assignment uses an obviously fake key to practice secret detection safely without exposing real credentials. A real key could give unauthorized access to accounts or services if it were accidentally committed to GitHub. The fake key helps us learn how to identify and prevent secret leaks without risking actual security.

---

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

<img width="1721" height="881" alt="Screenshot (216)" src="https://github.com/user-attachments/assets/5118d241-91fb-4147-8dd9-5ea24f747926" />


---

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

<img width="1920" height="397" alt="Screenshot (217)" src="https://github.com/user-attachments/assets/7801e56c-e44d-4151-8671-15857e359279" />


---

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

The hooks/pre-commit file is tracked in the repository so that all team members can share, review, and maintain the same hook script. Files inside .git/hooks/ are local to each developer's computer and are not included in Git commits. Keeping the hook in the repository makes it easier to share the script and set it up consistently across different computers.

---

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

The Git pre-commit hook intercepts a Git commit before it is created and can check for problems, such as accidentally staged secrets. If a problem is found, it can stop the commit.

The PreToolUse hook in Claude Code intercepts a tool call before Claude Code executes that tool. It can check the proposed action and help prevent unsafe operations.

Both act as safety checkpoints before an action happens. They help detect problems early and prevent unsafe actions from proceeding.

---

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

<img width="1715" height="221" alt="Screenshot (218)" src="https://github.com/user-attachments/assets/fe085c2b-048a-46f8-9f0f-b5cd4f0e7106" />


---

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The line that checks for the AKIA prefix matched my fake key because the key was created to look like an AWS access key. The hook detected the matching pattern in the staged file and displayed the BLOCKED message, preventing the commit. This shows how a pre-commit hook can help detect potential secrets before they enter the repository.

---

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

No, the hook might not detect a secret that does not contain the AKIA prefix or match its specific pattern. This shows that fixed rules can miss secrets that use different formats or names. Therefore, a pre-commit hook is a useful first line of defense, but it cannot guarantee that every secret will be detected.

---

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

<img width="1500" height="608" alt="Screenshot (219)" src="https://github.com/user-attachments/assets/9be157fe-8bc3-4ecc-9bd2-957c5d3700d1" />


---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

<img width="1334" height="990" alt="Screenshot (220)" src="https://github.com/user-attachments/assets/2b09725e-3753-4088-80e9-3788abd58f3e" />


---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

The /pr-ready skill uses Bash and Read to inspect staged changes and gather information about the code. It does not have Write permission because its job is only to analyze the changes and prepare a PR-readiness report and draft description. This helps prevent accidental file modifications and keeps the final decisions and actions under human control.

---

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

No, they did not necessarily flag the same things. The pre-commit hook checks for specific patterns, such as a fake AWS key with the AKIA prefix, and blocks the commit when a match is found. The /pr-ready skill performs a broader review and can flag potential secrets as well as debug statements. This shows that the pre-commit hook enforces fixed rules, while /pr-ready provides a more general review. Both help identify problems before changes are submitted.

---

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

<img width="1686" height="818" alt="Screenshot (221)" src="https://github.com/user-attachments/assets/230e10b9-c0c4-4a2f-ae2b-3eb59b77554d" />

---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

<img width="1393" height="812" alt="Screenshot (222)" src="https://github.com/user-attachments/assets/e0dff9a5-2d6b-4b77-8e2e-dcd9d34ccfa2" />


---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I removed the fake secret key and fixed the risky content in the staged file. Then I staged the corrected changes again and ran git commit. The pre-commit hook checked the changes and allowed the commit because the fake key pattern was no longer present.

---

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)



---

#### PR Link

Add your PR URL here...

---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

Add your answer here.

---

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

Add your answer here.

---

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

Add your answer here.

---

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

Add your answer here.

---

**2. Which step(s) represent Analyze?**

Add your answer here.

---

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

Add your answer here.

---

**4. Which step is Verify?**

Add your answer here.

---

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

Add your answer here.

---

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

Add your LinkedIn post URL here...

---

## Key Learnings

Add 3-5 bullet points on what you learned this week.

-
-
-

---

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

`Add your URL here`

---

# Completion Checklist

- [ ] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [ ] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [ ] `core.hooksPath` configured to point at `hooks/`
- [ ] Pre-commit hook shown blocking the risky commit
- [ ] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [ ] `/pr-ready` run against the risky diff and shown flagging issues
- [ ] Risky file fixed; `git commit` succeeds cleanly
- [ ] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [ ] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [ ] Agentic Loop mapping (Task 7) completed in your own words
- [ ] LinkedIn post published and URL submitted
- [ ] All required screenshots added
- [ ] GitHub repository URL provided

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
