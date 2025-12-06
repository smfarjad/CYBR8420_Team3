# Code Analysis for Software Security Engineering

---

## Part 1: Code Review Strategy and Execution

### 1. Code Review Strategy

Our team adopted a **hybrid code review strategy**, combining **scenario/weakness-based scoping** with a **checklist-based approach** focused on specific Common Weakness Enumerations (CWEs). This was supplemented by **automated static analysis** where tools were available.

#### Strategy Components:
1.  **Scope Definition (Scenario/Weakness-Based):** We prioritized code modules and files directly relevant to the high-risk areas identified in our **Misuse Cases**, **Assurance Claims**, and **Threat Models** from previous assignments. This focused our manual efforts on security-critical functions (e.g., authentication, input handling, encryption).
2.  **Checklist Focus (CWE-Based):** We created a targeted checklist of 5-10 specific CWEs most relevant to the project's **programming language** ([Language, e.g., Python, C++, JavaScript]), **platform**, and **architecture** to guide both manual and automated reviews.
3.  **Automated Scanning:** We selected and deployed relevant **Automated Static Application Security Testing (SAST)** tools based on the project's software composition.
4.  **Manual Review Enhancement:** For sections or languages not well-covered by automated tools, we conducted systematic manual reviews, utilizing **AI chatbot assistance** (as demonstrated in content module examples) to accelerate and refine the process.

### 2. Anticipated Challenges and Mitigation

| Challenge Expected | Strategy to Address the Challenge |
| :--- | :--- |
| **Codebase Size/Review Overload** | **Scope Definition:** Focusing only on files and modules critical to security functions identified in threat models. |
| **Missing Critical Bugs** | **Checklist Focus (CWEs):** Identifying specific, high-risk weakness types to ensure focused attention during review. |
| **Lack of Tool Availability/Effectiveness** | **Hybrid Approach:** Relying on systematic **Manual Code Review** where automated tools were unavailable or ineffective, including the use of AI assistance. |
| **Consistent Review Standards** | **Team Collaboration:** Ensuring all reviewers (Team Members 1-5) used the same defined CWE checklist and scope document. |

### 3. Manual Code Review Findings

* **Scope:** Review focused on:
    * **File:** `[e.g., src/auth/login.py]` - Authentication and Session Management
    * **File:** `[e.g., utils/input_validator.js]` - Input Validation and Sanitization
    * **File:** `[e.g., db/user_management.c]` - Data Handling/Database Interaction

| Finding ID | Location (File:Line) | Description of Vulnerability | CWE Mapping | Severity |
| :--- | :--- | :--- | :--- | :--- |
| MCR-001 | `src/auth/login.py:45` | Hardcoded secret key used for JWT signing/encryption. | CWE-798: Use of Hard-coded Credentials | High |
| MCR-002 | `utils/input_validator.js:12` | User input for `username` is not properly sanitized before being used in an HTML context. | CWE-79: Improper Neutralization of Input during Web Page Generation ('XSS') | Medium |
| MCR-003 | `db/user_management.c:101` | Use of `strcpy()` without bounds checking when copying user-supplied data into a fixed-size buffer. | CWE-120: Buffer Copy without Checking Size of Input ('Classic Buffer Overflow') | Critical |
| MCR-004 | [Add another finding or put N/A] | [Description] | [CWE] | [Severity] |

* **Total Manual Findings:** [Number]

### 4. Automated Code Scanning Findings

* **Tool(s) Used:** [e.g., Bandit (for Python), SonarQube (Trial), ESLint with Security Plugin]
* **Target:** [Specify which part of the codebase was scanned]

| Finding ID | Tool | Description of Vulnerability | CWE Mapping | Severity |
| :--- | :--- | :--- | :--- | :--- |
| ACR-001 | [Tool Name] | Potential SQL Injection due to unparameterized queries in `[File Name]`. | CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection') | Critical |
| ACR-002 | [Tool Name] | Detected insecure dependency version `[Package Name]` with a known vulnerability. | CWE-1104: Use of Unmaintained Third Party Component | High |
| ACR-003 | [Tool Name] | Missing security header (e.g., X-Content-Type-Options) in server configuration file. | CWE-16: Configuration | Low |

* **Link to Tool Output/Report:** [Insert Link to Report/Screenshot/Summary PDF Here]
* **Total Automated Findings:** [Number]

### Farjad:

### Joe:
### 1. Code Review Strategy (Joe)
The overall code review strategy was to experiment with different types of static analysis tools and evaluate whether their findings reinforced one another. Another key goal of the code review was to identify overlaps with previous assignments (threat model, misuse case, or assurance case). 

### 2. Anticipated Challenges and Mitigation

### Joe and Tyler:

### 3. Manual Code Review Findings
* **Scope:** Review focused on:
   * **Files:**
     - `[salt/master.py]` - Create Master Server
     - `[salt/auth]` - Authentication

| Finding ID | Location (File:Line) | Description of Vulnerability | CWE Mapping | Severity |
| :--- | :--- | :--- | :--- | :--- |
| MCR-001 | `salt/master.py:1665` | Path baypass if `..\` not caught in (clean Path) | CWE-22: Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal') | High |
| MCR-002 | `salt/master.py:373` | `Maintenance.handle_key_rptate` and multiple other systems check the same file for key rotations, which could change and cause denial of permissions. | CWE-362: Concurrent Execution using Shared Resource with Improper Synchronization ('Race Condition') | Medium |
| MCR-003 | `salt/auth/__init__.py:115` | The time_auth() function has no rate limiting, maximum attempt counts, or account lockout mechanisms. The technique shown above does add a small delay to each failure, but it is not a substitute for a robust lockout mechanism. The attacker is only slowed down by the delay, but they are not stopped from eventually guessing the password- making it susceptible to brute force attacks. This finding is also consistent with our earlier threat model, which identified the lack of built-in rate limiting as a potential vulnerability.   | CWE- 307: Improper Restriction of Excessive Authentication Attempts  | High |


### 4. Automated Code Scanning Findings

* **Tools Used:** Bandit, Semgrep, Snyk
* **Target:**
   - `[salt/master.py]` - Create Master Server
   - `[salt/auth/ldap]` - Authentication


| Finding ID | Tool | Description of Vulnerability | CWE Mapping | Severity |
| :--- | :--- | :--- | :--- | :--- |
| ACR-001 | Bandit | Try, Except, Pass detected. | CWE-703: Improper Check or Handling of Exceptional Conditions | Low |
| ACR-002 | Semgrep | Try, Except, Pass detected. | CWE-703: Improper Check or Handling of Exceptional Conditions | Low |
| ACR-003 | Synk and Semgrep | Environment() was created without enabling autoescape, this means that user input won’t be sanitized. If the username parameter contains malicious script content, it will be rendered directly into the template and executed in the user’s browser.   | CWE-79: Cross-Site Scripting | Medium |

* **Link to Tool Output/Report:**
    - ACR-001 - [Bandit Report](https://github.com/smfarjad/CYBR8420_Team3/blob/assignment5-Tyler/Automated%20Reports/Screenshot%202025-12-05%20203228.png)
    - ACR-002 - [Semgrep Report](https://github.com/smfarjad/CYBR8420_Team3/blob/assignment5-Tyler/Automated%20Reports/Semgrep_Code_Findings_2025_12_06.csv)
    - ACR-003 - [Semgrep Report](https://semgrep.dev/orgs/josephnguyen719/findings/460996609) and [Snyk Report](https://app.snyk.io/org/joe-nguyenn/project/4e92fa28-e3ef-4f9a-8818-5b9198cab132#issue-8ce57638-586f-4be7-923a-1177ca6b413c) 


---

## Part 2: Key Findings and Contributions

| CWE ID | Description of Significant Finding(s) | Perceived Risk in Operational Environment |
| :--- | :--- | :--- |
| **CWE-79** | **Cross-Site Scripting:** Automated scanning detected that the code is using a Jinja2's Environment() without enabling auto-escaping. | In an enterprise environment, a XSS vulnerability enables account compromise, data exfiltration, internal phishing, and lateral movement across interconnected systems. |
| **CWE-307** | **Brute Force Attack:** Manual scanning detected that the system does not enforce limits on repeated authentication attempts. The time_auth() function attempts to slow brute-force attacks by adding a uniform delay but does not enforce actual rate limits or lockouts. | This creates a high risk of brute-force attacks, making it easier for attackers to compromise accounts and gain unauthorized access in an enterprise environment|
| **CWE-22** | **Path Traversal:** The manual review identified a possiblility for Path Traversal. | **Critical Risk:** Potential for traversal to unguarded portions of the code/file structure with the input of a new path that would be executed. |
| **CWE-362** | **Race Condition:** The manual review identified a possiblility for Race Condition. | **High Risk:** Potential for an attacker to manipulate the key rotation as multiple file pulls from the same key file rotations. |
| **CWE-703** | **Improper Check or Handling of Exceptional Conditions:** Automated scanning detected multiple Improper Check or Handling of Exceptional Conditions. | **Low Risk:** This rarely does not anticipates how an exception could occur. |

### 2. Planned or Ongoing Contributions to the Upstream Open-Source Project

* **Farjad:**
* **Joe:** I plan to contribute by improving the documentation for SaltStack's authentication process. This includes clarifying how token handling, rate-limiting, and authentication checks operate so new users and developers can better understand the system. 
* **Inser Name:**
* **Tyler:** For the future, I plan to look more into the documentation and possibly make a step-by-step guide to enable different security features, as not all of them are turned on to begin with. This could then be implemented into the getting-started documentation. 


**Overall Assessment:** The project overall is very well put together with only a couple of places that need to be fixed.



### 3. Team GitHub Repository Link



---

## Team Reflection on Learning

### Team Summary Reflection


### Individual Team Member Reflections

#### Team Member 1: Farjad
* **What I learned:** 
* **Most Useful:** 

#### Team Member 2: Joe
I learned how valuable static analysis tools can be when reviewing large and coomplex codebase like Salt. The tools are most effective when combined with a clear review strategy. I also learned that using multiple static analysis tools will render very different results, making it important to compare them and verify which findings are truly meaningful. What I found most useful was discovering how much overlap exists between the previous assignments we created earlier and the actual security gaps in the code. 
  
#### Team Member 3: [Name]
* **What I learned:** 
* **Most Useful:** 

#### Team Member 4: Tyler
* **What I learned:** For this assignment, I learned how to manuly perform a code assesment. This a taught me what coding practices I need to change personally to create secure code that I would feel safe deploying for others to view. This is a good habit to get into as it will save time and money when developing for a client in the future. 
* **Most Useful:** The most useful item I learned for this assignment is the mindset to get into and the questions to ask when developing secure code. This will help me save time when developing code in the future. 

#### Team Member 5: [Name]
* **What I learned:** 
* **Most Useful:** 
