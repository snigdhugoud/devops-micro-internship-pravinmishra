# Assignment 5 — AI-Assisted Sprint Health Report via Jira MCP

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will connect Claude Code to your Jira board through an MCP server, the same way you connected it to GitHub in Week 2, and build a read-only `/sprint-health` skill. The skill reads your current sprint through Jira's API and reports sprint velocity, stories at risk of missing the sprint, and items missing an estimate — but it must never create, edit, comment on, or transition a single ticket itself. You will prove that boundary holds by making a real change on the board yourself and confirming the skill only ever reports, never acts.

---

# Task 1 — Create a Jira API Token

## Goal

Generate an API token from your Atlassian account that the MCP server will use to authenticate with your Jira site. Do not screenshot the token value itself.

### Evidence

#### Screenshot 1 — Jira API token creation confirmation page showing the token name, with the token value not visible

<img width="1920" height="883" alt="Screenshot (277)" src="https://github.com/user-attachments/assets/b3d07835-c94a-4ac3-818a-55360ec46baf" />


### Notes You Must Write (Very Important):

Why does the MCP server need your site URL and account email in addition to the token?

The MCP server needs the Jira site URL, Atlassian account email, and API token to connect securely to Jira. The site URL identifies the Jira instance, the email identifies the Atlassian account, and the API token authenticates the connection. Together, these details allow the MCP server to access Jira data and perform permitted actions according to the account’s permissions.

---

# Task 2 — Create .mcp.json at the Project Root

## Goal

Create or update `.mcp.json` at your project root with a Jira MCP server block, following the same shape as the GitHub MCP server you configured in Week 2.

### Evidence

#### Screenshot 2 — `.mcp.json` open in VS Code showing the Jira server configuration

<img width="1420" height="962" alt="Screenshot (279)" src="https://github.com/user-attachments/assets/a223cafe-ed13-4914-a899-4e28fa040e48" />


### Notes You Must Write (Very Important):

Compare this jira block to the github block from Week 2 Assignment 5. The GitHub server ran via npx (a Node.js package); this one runs via uvx (a Python package) — what stays exactly the same shape despite that difference, and why doesn't Claude Code care which language a given MCP server is written in?

The Jira and GitHub MCP configuration blocks have the same overall structure: both specify the server name, the command to run, and the arguments needed to start the server. The main difference is that the GitHub server uses npx to run a Node.js package, while the Jira server uses uvx to run a Python package. Claude Code does not care which programming language the server uses because MCP provides a standard communication protocol that allows different tools and servers to communicate in the same way.

---

# Task 3 — Add Your Credentials to settings.local.json

## Goal

Add your Jira site URL, account email, and API token to `.claude/settings.local.json`, and confirm that file is listed in `.gitignore` so it is never committed.

### Evidence

#### Screenshot 3 — `settings.local.json` open in VS Code showing the `env` section, with the actual token value blurred or covered

<img width="1396" height="968" alt="Screenshot (281)" src="https://github.com/user-attachments/assets/77842dd7-7698-4fa6-aa6f-e0117a2d059e" />


### Notes You Must Write (Very Important):

Why must JIRA_API_TOKEN live in settings.local.json and never in .mcp.json?

JIRA_API_TOKEN must be stored in .claude/settings.local.json because it contains a secret credential used to authenticate with Jira. This file is intended for local settings and should be listed in .gitignore so it is not committed to GitHub. The .mcp.json file is used to configure the MCP server, not to store private credentials. Keeping the token out of .mcp.json helps prevent accidental exposure of sensitive information when sharing or committing project files.
---

# Task 4 — Verify the Connection with /mcp

## Goal

Restart Claude Code and confirm the Jira MCP server shows as connected.

### Evidence

#### Screenshot 4 — `/mcp` output showing `jira: connected`

<img width="1057" height="518" alt="Screenshot (282)" src="https://github.com/user-attachments/assets/fb8ed217-bc7d-47f5-9bc3-94b81e62a53f" />


---

# Task 5 — Run a Live Query to Prove Real Board Data

## Goal

Ask Claude to list the issues in your current active sprint through the Jira MCP connection, and confirm the result matches what you see on your live board in the browser.

### Evidence

#### Screenshot 5 — Claude's response showing the live sprint issue list retrieved via Jira MCP

<img width="1453" height="488" alt="Screenshot (283)" src="https://github.com/user-attachments/assets/d6f7680e-6f55-4a9a-b310-800050ea8cba" />


### Notes You Must Write (Very Important):

How did you confirm this was real board data and not something Claude guessed?

I confirmed that the data was real by using the Jira MCP connection in Claude Code to retrieve issues from my project's active sprint. I checked the issue keys, summaries, statuses, assignees, story points, and priorities against the actual sprint board in my Jira browser. I also compared the issue count and status totals. Since the results matched the live Jira board, I verified that Claude used real board data rather than guessing or generating sample information.

---

# Task 6 — Build the /sprint-health Skill

## Goal

Create a `/sprint-health` skill restricted to read-only Jira tools plus `Read`, with no issue-mutating tools and no `Write`. Run it and confirm it produces a report covering sprint velocity, at-risk stories, and items missing an estimate.

### Evidence

#### Screenshot 6 — `SKILL.md` frontmatter showing `allowed-tools` limited to read-only Jira tools plus `Read`, with `disable-model-invocation: true`

<img width="1920" height="970" alt="Screenshot (284)" src="https://github.com/user-attachments/assets/b1d7ec26-4f0d-4306-b724-0c328d33b540" />


#### Screenshot 7 — `/sprint-health` output showing the full triage report against your real sprint

<img width="445" height="934" alt="Screenshot (285)" src="https://github.com/user-attachments/assets/d2868f45-d708-46d0-b925-96d5a263a466" />


### Notes You Must Write (Very Important):

1. Which Jira MCP tools does this skill's allowed-tools list include, and which mutating tools (create issue, update issue, transition issue, add comment) does it deliberately exclude?

The allowed-tools list includes four read-only Jira MCP tools: mcp__jira__jira_search, mcp__jira__jira_get_issue, mcp__jira__jira_get_sprint, and mcp__jira__jira_get_board, along with the Read tool. It deliberately excludes mutating tools such as create issue, update issue, transition issue, and add comment. This ensures the skill can inspect sprint data and generate a report without changing the Jira board.

2. Why does a Scrum Master need this restriction more than almost any other role in this course?

A Scrum Master helps the team maintain transparency, inspect progress, and adapt the sprint plan collaboratively. Automatically changing issues, transitioning statuses, or adding comments could interfere with the team's workflow and create inaccurate records. A read-only skill provides evidence-based sprint health information while leaving decisions and actions to the Scrum Master and team.
---

# Task 7 — Prove the Skill Never Mutates the Board

## Goal

Manually update one ticket on your board in the browser (for example, move a story to "Done" or add a missing estimate), then run `/sprint-health` again and confirm the new report reflects your change — proving the skill only ever reads live state and never wrote to the board itself.

### Evidence

#### Screenshot 8 — Second `/sprint-health` run showing the report now reflects your manual board change

<img width="1357" height="962" alt="Screenshot (286)" src="https://github.com/user-attachments/assets/6f994c22-400c-47cf-916d-323dd7205c58" />


### Notes You Must Write (Very Important):

Map this assignment to Gather → Analyze → Human Act → Verify from Week 3 Assignment 6. Which step did you perform manually in the browser, and why must that step stay human?

The workflow maps to Gather → Analyze → Human Act → Verify as follows:
1. Gather: Claude Code retrieves live sprint and issue data using Jira MCP read-only tools.
2. Analyze: The /sprint-health skill analyzes sprint velocity, at-risk stories, missing estimates, and acceptance criteria.
3. Human Act: I manually updated a Jira Story in the browser by changing its status or adding a story point estimate. This step must remain human because the Scrum Master and team are responsible for making decisions, confirming work is complete, and maintaining accurate Jira records. Automation should provide evidence and recommendations, not make unauthorized changes.
4. Verify: I ran /sprint-health again and checked whether the report reflected my manual change.

---

# Submission Instructions

Complete all tasks in sequence.

Your submission must include:
- All 8 required screenshots
- All the required notes

---

# Completion Checklist

- [ ] Task 1: Jira API token created, value never screenshotted (Screenshot 1)
- [ ] Task 2: `.mcp.json` has the Jira server block (Screenshot 2)
- [ ] Task 3: Credentials stored in `settings.local.json`, token blurred, file gitignored (Screenshot 3)
- [ ] Task 4: `/mcp` shows the Jira server connected (Screenshot 4)
- [ ] Task 5: Live query returned real sprint data, verified against the browser (Screenshot 5)
- [ ] Task 6: `/sprint-health` skill created with correct read-only `allowed-tools`, and produced a full report (Screenshots 6–7)
- [ ] Task 7: A manual board change was reflected in a second `/sprint-health` run (Screenshot 8)
- [ ] Skill never created, edited, transitioned, or commented on any issue
- [ ] Reflection answered (Notes)
- [ ] No API token value exposed

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
