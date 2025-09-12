# Project Proposal: Team 3

This document outlines our team's proposal for the project, focusing on the security analysis of a chosen open-source software.

---

### **1. Team Collaboration & Project Management**

**Public GitHub Repository:**
https://github.com/smfarjad/CYBR8420_Team3

**GitHub Project Board:**
https://github.com/users/smfarjad/projects/3

---

### **2. Open-Source Software Selection**

**Software Name:**
Salt

**Repository Link:**
https://github.com/saltstack/salt

---

### **3. Hypothetical Operational Environment & Security Analysis**

**Operational Environment Description:**
[Describe a hypothetical setting, such as a home, office, or enterprise, where the software would be used. Detail the type of users, the kind of data they handle, and the software's role in this environment.]

**Systems Engineering View Diagram:**
[Insert a link to or embed an image of your systems engineering diagram here. The diagram should visually represent the software in its operational environment, showing its interactions with users and other systems.]

**Threats:**
[List the perceived threats to the software in the described environment. Consider potential attackers, their motivations, and the vulnerabilities they might exploit. For example:
- **Threat 1:** Unauthorized access to user data.
- **Threat 2:** Denial of service attacks against the application.
- **Threat 3:** Data tampering.]

**Security Features:**
[List the security features you have identified in the software. For example:
- **Feature 1:** End-to-end encryption for all data.
- **Feature 2:** Role-based access control.
- **Feature 3:** Secure password hashing and storage.]

---

### **4. Project Motivation & Description**

**Team Motivation for Selection:**
We chose Salt for the project because it offers a rich setting in which to explore software assurance: it’s relevant to current trends in infrastructure automation and DevOps, poses clear challenges around security, consistency, and reliability, and gives us opportunities for hands-on work with real tools used in production environments.

**Open-Source Project Description:**
- **What is it?**: Salt (also known as SaltStack) is an event-driven automation and configuration management framework. It is used to deploy, configure, and manage complex IT systems, ensuring that all components maintain a consistent desired state.
- **Contributors**: The project has more than 3,000 contributors in its community.  [Number of contributors and a note on community activity.]
- **Activity**: Releases are made frequently; feature releases occur every 4-6 weeks with subsequent bugfix or maintenance releases. There is substantial ongoing community maintenance, active issue tracking, and contributions via pull requests. 
- **Use & Popularity**:  Salt is widely used in industry for infrastructure management, configuration drift prevention, orchestration, and automating routine tasks. It is considered one of the mature tools alongside Puppet, Chef, Ansible. 
- **Languages Used**: Primarily Python. Configuration files/states are often written in YAML with support via templating (e.g. Jinja) etc. [List the primary programming languages used in the project.]
- **Platform**: Salt runs on Unix-like systems (Linux, BSD), macOS, and Windows. It manages servers, containers, virtual machines, databases, network devices, etc. 
- **Documentation Sources**: docs.saltproject.io

**Additional Project Statistics:**

- **Number of contributors:** Salt has more than 3,000 contributors to its GitHub repository. 
GitHub

- **Total commits:** The repository has over 108,300 commits on the main Salt repo. 
docs.saltproject.io

- **Open issues:** As of early September 2025, there are thousands of open issues—e.g. issues numbered in the 68,000s (e.g. #68311, #68308, etc.). 
GitHub

- **Recent activity:** Salt continues to have regular bug reports and pull requests. It also had a recent Long Term Support (LTS) release (v3006.10) in March 2025.

---

### **5. License & Contribution Procedures**

**Software License:**
[Identify the open-source license (e.g., MIT, GPLv3). Provide a brief summary of what the license permits or restricts.]

**Contribution Procedures & Contributor Agreements:**
[Describe the process for making a contribution to the project. Mention if a Contributor License Agreement (CLA) is required and how a new developer would submit a pull request.]

---

### **6. Security History & Team Reflection**

**Security-Related History:**

The Adversarial Robustness Toolbox (ART) has had a few security-related vulnerabilities. The vulnerabilities were tied to external dependencies rather than its own codebase.  

**CVE-2021-28678**  

-Affected ART versions prior to 1.6.1 due to a vulnerable Pillow dependency 

-Fixed in version 1.6.1, updated to a secure version  

**CVE-2021-34552**  

-Also linked to Pillow 

-Remediated in version 1.7.1, updated to a secure version 

**CVE-2021-23437** 

-Dependency flaws linked to Pillow

-Resolved in version 1.8.0, updated to a secure version 

The latest version 1.19.1 (January 22, 2025) has no known security vulnerabilities.  



**Team Reflection:**


***Mohammed Alfawzan***
- **What did you learn?**: [Your personal learning experience from this assignment.]
- **What did you find most useful?**: [The most valuable part of the process for you.]

***Sheikh Muhammad Farjad***
- **What did you learn?**: [Your personal learning experience from this assignment.]
- **What did you find most useful?**: [The most valuable part of the process for you.]

***Tyler McCoid***
- **What did you learn?**: [Your personal learning experience from this assignment.]
- **What did you find most useful?**: [The most valuable part of the process for you.]

***Joe Nguyen***
- **What did you learn?**: [Your personal learning experience from this assignment.]
- **What did you find most useful?**: [The most valuable part of the process for you.]

***John Winchester***
- **What did you learn?**: [Your personal learning experience from this assignment.]
- **What did you find most useful?**: [The most valuable part of the process for you.]
