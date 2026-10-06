# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

<img width="1920" height="582" alt="Screenshot (140)" src="https://github.com/user-attachments/assets/e7b9e411-c66b-45f3-b45b-05e3fbdc9aa0" />


---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

<img width="1920" height="1080" alt="Screenshot (141)" src="https://github.com/user-attachments/assets/d1f16931-ff76-4719-96b0-bf255d716b24" />


---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash stands for Bourne Again Shell. It is a command-line shell used in Linux and other operating systems to run commands and scripts. It also provides features for automating tasks using Bash scripts.

---

**2. What is the difference between shell and Bash?**

A shell is a general program that allows users to interact with the operating system through commands. Bash is one specific type of shell. Other shells include Zsh, Fish, and Dash.

---

**3. Why is it important to confirm the Bash version before writing scripts?**

Different Bash versions can support different features and syntax. Checking the version helps ensure that the commands and features used in a script will work correctly on the target system and avoids compatibility problems.

---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

<img width="1920" height="561" alt="Screenshot (142)" src="https://github.com/user-attachments/assets/2b99de14-cf9c-4a82-b3b7-52a899e4422f" />


---

#### Screenshot 2 — Output of `./first-script.sh`

<img width="1700" height="361" alt="Screenshot (143)" src="https://github.com/user-attachments/assets/e80a4e3d-b92e-45ea-abf4-c41481fc6ecd" />


---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

<img width="1786" height="323" alt="Screenshot (144)" src="https://github.com/user-attachments/assets/ed99bdef-b101-4fe5-baf8-55d87be3f5b0" />


---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

#!/bin/bash tells the operating system to use the Bash shell to execute the script. It is called a shebang or hashbang.

---

**2. Why do we use `chmod +x` before running a script?**

chmod +x gives the script execute permission. This allows us to run the script directly using ./script.sh.

---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

./script.sh runs the script directly and requires execute permission. bash script.sh tells Bash to run the script directly, so execute permission is not required.

---

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

<img width="1920" height="1080" alt="Screenshot (146)" src="https://github.com/user-attachments/assets/543b0f82-6792-41c4-a490-5813e92ed1f6" />


---

#### Screenshot 2 — Output of `./user-info.sh`

<img width="1680" height="493" alt="Screenshot (145)" src="https://github.com/user-attachments/assets/48358e49-98f9-4f59-94ae-812d147cfe2a" />


---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable in Bash is a name used to store a value, such as text, numbers, or other information, so it can be used later in a script.

---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

We should avoid spaces around the = sign because Bash requires the variable assignment to be written without spaces. For example, name="snigdhugoud" is correct

---

**3. How do you access the value stored inside a Bash variable?**

You can access the value of a Bash variable by putting $ before the variable name.

Example: echo $name

---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

<img width="1920" height="1080" alt="Screenshot (148)" src="https://github.com/user-attachments/assets/6ec8b5cf-4818-4309-bf98-535de99f7d02" />


---

#### Screenshot 2 — Output of `./tools-checklist.sh`

<img width="1740" height="420" alt="Screenshot (147)" src="https://github.com/user-attachments/assets/71f3173c-79cd-41e8-a24a-15edfa200e83" />


---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array is a variable that stores multiple values.

---

**2. Why are arrays useful in scripts?**

Arrays are useful for storing and managing multiple related values together.

---

**3. What does `"${tools[@]}"` mean?**

It means all the values stored in the tools array.

---

**4. What is the purpose of the `for` loop in this script?**

The for loop goes through each tool in the array and displays it.

---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

<img width="978" height="1080" alt="Screenshot (149)" src="https://github.com/user-attachments/assets/43b75cea-c9b6-41fd-9861-181ee7082580" />


---

#### Screenshot 2 — Output of `./counter.sh`

<img width="1727" height="280" alt="Screenshot (150)" src="https://github.com/user-attachments/assets/60625402-d805-47db-86d7-8719016c9660" />


---

### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop repeats a set of commands multiple times.

---

**2. Why do we use loops in Bash scripting?**

We use loops to perform the same task repeatedly without writing the same commands again.

---

**3. How many times did the loop run in your script?**

The loop ran 5 times.

---

**4. What would you change if you wanted the loop to run 10 times?**

I would change the numbers from 1 2 3 4 5 to 1 2 3 4 5 6 7 8 9 10.

---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

<img width="1859" height="254" alt="Screenshot (151)" src="https://github.com/user-attachments/assets/f7a964b5-a90f-4eef-858f-81ce124f3968" />


---

#### Screenshot 2 — Content of `file-check.sh`

<img width="1920" height="1080" alt="Screenshot (152)" src="https://github.com/user-attachments/assets/7f7a0d8e-4781-4034-9d08-87355a33100a" />


---

#### Screenshot 3 — Output of `./file-check.sh`

<img width="1674" height="174" alt="Screenshot (153)" src="https://github.com/user-attachments/assets/38f8d1d7-21a7-4a03-a951-8441a5a47dd3" />


---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

-d checks whether a directory exists.

---

**2. What does `-f` check in Bash?**

-f checks whether a file exists.

---

**3. Why should file and directory paths be stored in variables?**

It makes the script easier to read and update.

---

**4. What happens if the file does not exist?**
The else condition runs and displays that the file does not exist.



---

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

<img width="1920" height="1080" alt="Screenshot (156)" src="https://github.com/user-attachments/assets/3190b52f-c32a-4e68-8c12-0e749a7e7974" />



---

#### Screenshot 2 — Output showing `Result: Pass`


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a6daf7ac-bb85-4e96-adb7-1a00d96ffc27" />


---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

<img width="1920" height="1080" alt="Screenshot (154)" src="https://github.com/user-attachments/assets/73f217b1-c481-4d21-9cc0-409b2c288d37" />

---

#### Screenshot 4 — Output showing `Result: Retry`

<img width="932" height="97" alt="Screenshot (155)" src="https://github.com/user-attachments/assets/fb1b96fd-13a9-4495-9016-f2bcecccd43b" />


---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

It is used to make decisions based on a condition.

---

**2. What does `-ge` mean?**

-ge means greater than or equal to.

---

**3. Why should conditions be tested with different values?**

To make sure the script works correctly in different situations.

---

**4. How can conditionals help in automation scripts?**

They allow scripts to take different actions depending on the situation.

---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`


<img width="1920" height="1080" alt="Screenshot (158)" src="https://github.com/user-attachments/assets/fdc596f5-292b-4775-a397-b4823303d0e4" />


---

#### Screenshot 2 — Output of `./final-automation.sh`


<img width="1920" height="561" alt="Screenshot (157)" src="https://github.com/user-attachments/assets/1855aca2-917a-4987-943b-d94ec695e2da" />


---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts


<img width="338" height="56" alt="image" src="https://github.com/user-attachments/assets/a4c4f5a3-9ced-4596-b3dd-00fc50a8a52e" />


---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

A function is a block of commands that performs a specific task.

---

**2. Why are functions useful in scripts?**

Functions make scripts easier to organize, reuse, and understand.

---

**3. Which functions did you create in this script?**

I created print_header, print_user_details, check_files, and print_tools.

---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

The script uses variables for information, an array for tools, a loop to display tools, conditionals to check files and directories, and functions to organize the tasks.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://lnkd.in/p/dRBuj2r6

---

#### Screenshot — Published LinkedIn post


<img width="1920" height="1080" alt="Screenshot (159)" src="https://github.com/user-attachments/assets/3c03f982-4fa3-42bb-a402-1ed41f44f080" />


---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [✅] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [✅] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [✅] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [✅] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [✅] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [✅] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [✅] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [✅] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [✅] All scripts run without errors
- [✅] Full Name visible in all required screenshots
- [✅] LinkedIn post published and URL submitted
- [✅] No sensitive data exposed

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
