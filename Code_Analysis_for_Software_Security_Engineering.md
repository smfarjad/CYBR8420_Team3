# Code Analysis for Software Security Engineering

---

## Part 1: Code Review Strategy and Execution

### Code Review Strategy

Our team adopted a **hybrid code review strategy** that combined **scenario and weakness-based scoping** with a **checklist approach** centered on selected Common Weakness Enumerations (CWEs). This process was supported by **automated static analysis** when appropriate tools were available.

#### Strategy Components:
1. **Scope Definition (Scenario and Weakness-Based):** We began by prioritizing code modules and files that align with the high-risk areas identified in our Misuse Cases, Assurance Claims, and Threat Models from previous assignments. This allowed us to focus manual review efforts on security-critical functionality such as authentication, input handling, and encryption.

2. **Checklist Focus (CWE-Based):** Once the scope was defined, we prepared a list of CWEs that are most relevant to our operational environment and the analysis we have performed throughout the course. The complete list of CWEs is provided in the next section.

3. **Automated Scanning:** After selecting the modules and the corresponding CWE list, we conducted automated scans. Each team member used tools they were comfortable with, and we ensured that multiple tools were employed to reduce discrepancies in their findings.

4. **Manual Review:** Following the automated scans, we conducted a manual review. This served two purposes: (a) to validate the results produced by automated tools, and (b) to identify issues that automated scanning may have overlooked.


### List of CWEs
- **Input Validation / Trust Boundary / Data Handling**
  - CWE-22: Path Traversal
  - CWE-79: Improper Neutralization of Input During Web Page Generation (Cross-Site Scripting)
  - CWE-345: Insufficient Verification of Data Authenticity
  - CWE-347: Improper Verification of Cryptographic Signature
  - CWE-501: Trust Boundary Violation

- **Authorization / Access Control**
  - CWE-552: Files or Directories Accessible to External Parties
  - CWE-732: Incorrect Permission Assignment for Critical Resource

- **Authentication / Session Management**
  - CWE-307: Improper Restriction of Excessive Authentication Attempts
  - CWE-522: Insufficiently Protected Credentials

- **Information Exposure**
  - CWE-200: Exposure of Sensitive Information to an Unauthorized Actor

- **Cryptographic / Randomness Issues**
  - CWE-330: Use of Insufficiently Random Values

- **Concurrency / Race Conditions**
  - CWE-362: Race Condition

- **Error Handling / Logging**
  - CWE-703: Improper Handling of Exceptional Conditions

### Manual Code Review Findings
* **Scope:** Review focused on:
   * **Files/Directories:**
     - `[salt/master.py]` - Create Master Server
     - `[salt/auth]` - Authentication
     - `[salt/state.py]` - Salt state engine for applying remote deployments
     - `[salt/noxfile.py]` - Nox config used to run Salt tasks/tests (build/CI config)
     - `[salt/pillar/]` - Pillar operations

| Finding ID | Location (File:Line) | Description of Vulnerability | CWE Mapping | Severity |
| :--- | :--- | :--- | :--- | :--- |
| MCR-001 | `salt/master.py:1665` | Path baypass if `..\` not caught in (clean Path) | CWE-22: Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal') | High |
| MCR-002 | `salt/master.py:373` | `Maintenance.handle_key_rptate` and multiple other systems check the same file for key rotations, which could change and cause denial of permissions. | CWE-362: Concurrent Execution using Shared Resource with Improper Synchronization ('Race Condition') | Medium |
| MCR-003 | `salt/auth/__init__.py:115` | The time_auth() function has no rate limiting, maximum attempt counts, or account lockout mechanisms. The technique shown above does add a small delay to each failure, but it is not a substitute for a robust lockout mechanism. The attacker is only slowed down by the delay, but they are not stopped from eventually guessing the password- making it susceptible to brute force attacks. This finding is also consistent with our earlier threat model, which identified the lack of built-in rate limiting as a potential vulnerability.   | CWE- 307: Improper Restriction of Excessive Authentication Attempts  | High |
| MCR-005 | `state.py:1961, 2312` | Uses random.randint() to add “splay” to retry intervals. Standard PRNG is not suitable for security-critical randomness, but here it only affects timing. | CWE-330: Use of Insufficiently Random Values | Low |
| MCR-006 | `noxfile.py:197` | Uses assert for argument checking. Assertions can be disabled in optimized Python, so relying on them for validation is fragile. | CWE-703: Improper Handling of Exceptional Conditions | Low |
| MCR-007 | `localfs.py:write_token` | Token files are stored in plaintext and contain user metadata, exposing sensitive information if the filesystem is compromised. | CWE-200 | Medium |
| MCR-008 | `localfs.py:read_token` | Token contents are trusted without authenticity checks; a forged token file could escalate privileges or impersonate users. | CWE-345 | High |
| MCR-009 | `__init__.py:validate_token` | Authorization relies solely on token-embedded attributes without revalidating user roles, allowing privilege persistence after role changes. | CWE-285 | High |
| MCR-010 | `salt/pillar/__init__.py:~125–140, ~260–300` | The master accepts pillarenv supplied by the minion and overwrites its own environment selection, allowing a minion to request pillar data from another environment (e.g., production, staging, secrets). This violates the trust boundary and may expose sensitive pillar data to unauthorized minions. | CWE-501: Trust Boundary Violation | High |
| MCR-011 | `salt/pillar/__init__.py:~760–780` | When `pillar_opts=True`, the master includes its internal configuration (opts) inside the pillar data returned to minions. This reveals sensitive master settings such as directory paths, environment mappings, enabled backends, and operational metadata to any minion that requests pillar, which results in unintended information exposure. | CWE-200: Exposure of Sensitive Information to an Unauthorized Actor / CWE-552: Filesystem Exposure | High |


### Automated Code Scanning Findings

* **Tools Used:** Bandit, Semgrep, Snyk
* **Target:**
   - `[salt/master.py]` - Create Master Server
   - `[salt/auth/ldap]` - Authentication
   - `[salt/state.py]` - Salt state engine for applying remote deployments.
   - `[salt/noxfile.py] `- Nox config used to run Salt tasks/tests (build/CI config)

| Finding ID | Tool | Description of Vulnerability | CWE Mapping | Severity |
| :--- | :--- | :--- | :--- | :--- |
| ACR-001 | Bandit | There are some rare cases where the channel.close() function might have an exception that does not close correctly.  | CWE-703: Improper Check or Handling of Exceptional Conditions | Low |
| ACR-002 | Bandit | There are some rare cases where the clear_funcs.destroy() function might have an exception that does not close correctly. | CWE-703: Improper Check or Handling of Exceptional Conditions | Low |
| ACR-003 | Synk and Semgrep | Environment() was created without enabling autoescape, this means that user input won’t be sanitized. If the username parameter contains malicious script content, it will be rendered directly into the template and executed in the user’s browser.   | CWE-79: Cross-Site Scripting | Medium |
| ACR-004 | Bandit | On state.py and noxfile.py, Bandit reported Low-severity issues: pickle import, random.randint() for retry splay, and assert checks. | CWE-502, CWE-330, CWE-703 | Low |

* **Link to Tool Output/Report:**
    - ACR-001 & ARC-002 - [Bandit Report](https://github.com/smfarjad/CYBR8420_Team3/blob/assignment5-Tyler/Automated%20Reports/Screenshot%202025-12-05%20203228.png)
    - ACR-003 - [Semgrep Report](https://semgrep.dev/orgs/josephnguyen719/findings/460996609) and [Snyk Report](https://app.snyk.io/org/joe-nguyenn/project/4e92fa28-e3ef-4f9a-8818-5b9198cab132#issue-8ce57638-586f-4be7-923a-1177ca6b413c) 
    - ACR-004 – [Bandit report](https://github.com/smfarjad/CYBR8420_Team3/blob/main/Automated%20Reports/image_2025-12-06_142028932.png)

---

## Part 2: Key Findings and Contributions

*Operational Environment: Edge-based monitoring systems operating in critical regions.*

| CWE ID | Description of Significant Finding(s) | Perceived Risk in Operational Environment |
| :--- | :--- | :--- |
| **CWE-22** | **Path Traversal:** The manual review identified a possiblility for Path Traversal. | **Critical Risk:** Potential for traversal to unguarded portions of the code/file structure with the input of a new path that would be executed. |
| **CWE-79** | **Cross-Site Scripting:** Automated scanning detected that the code is using a Jinja2's Environment() without enabling auto-escaping. | In an enterprise environment, a XSS vulnerability enables account compromise, data exfiltration, internal phishing, and lateral movement across interconnected systems. |
| **CWE-307** | **Brute Force Attack:** Manual scanning detected that the system does not enforce limits on repeated authentication attempts. The time_auth() function attempts to slow brute-force attacks by adding a uniform delay but does not enforce actual rate limits or lockouts. | This creates a high risk of brute-force attacks, making it easier for attackers to compromise accounts and gain unauthorized access in an enterprise environment|
| **CWE-330** | Insufficiently Random Values: state.py uses random.randint() to jitter retry intervals (“splay”). This is not cryptographically secure randomness, but it only affects timing behaviour. | Low operational risk today because it does not protect secrets; however, it shows that non-crypto PRNGs are used and should be avoided in security-critical contexts. |
| **CWE-362** | **Race Condition:** The manual review identified a possiblility for Race Condition. | **High Risk:** Potential for an attacker to manipulate the key rotation as multiple file pulls from the same key file rotations. |
| **CWE-501** | Trust Boundary Violation: Manual review identified that the master accepts the pillarenv value supplied by the minion and updates its internal configuration with it. This allows a minion to request pillar from alternate environments such as production, staging, or secret environments, which violates Salt’s trust model. | **High Risk:** In an operational deployment this could expose confidential pillar data to unauthorized minions. A misconfigured or malicious minion could retrieve secret configurations or credentials from environments that it should not have access to, leading to privilege escalation and unintended disclosure. |
| **CWE-502** | Unsafe Deserialization: Bandit and manual review flagged use of pickle in state.py. If untrusted data ever reaches this deserialization, it could allow arbitrary code execution. Currently used for internal data, but it remains a potential risk. | In a real deployment, any misuse of pickle with network or user-supplied data would be a high risk, allowing remote code execution on Salt master/minion nodes. |
| **CWE-200 / CWE-552** | Information Exposure: When `pillar_opts=True`, the master places its internal configuration (`opts`) inside the pillar data returned to minions. This includes sensitive operational parameters such as file paths, enabled backends, and environment mappings. | **High Risk:** In an enterprise environment this leaks internal configuration details to all minions, increasing the attacker’s understanding of master internals. Such information can assist lateral movement, targeted attacks against backends, or precise exploitation of master configuration weaknesses. |
| **CWE-703** | **Improper Handling of Exceptional Conditions:** Automated scanning identified multiple locations where exceptions are caught or suppressed without appropriate handling. This can hide failures and make debugging or operational diagnosis difficult. | **Low Risk:** These cases do not directly expose the system to attack, but they reduce reliability and observability, which can hinder incident response or troubleshooting. |
| **CWE-703** | **Improper Handling of Exceptional Conditions:** Use of `assert` statements in production code (`noxfile.py`). Assertions are removed when Python runs with optimization flags, causing validation logic to disappear entirely. | **Low Risk:** If deployed with optimization flags or repackaged downstream, required checks would no longer execute, enabling incorrect inputs or invalid states that violate assumptions made in security or functional assurance. |


### Planned Contributions to Salt
As a team, we plan to strengthen SaltStack by improving several areas where clarity and reliability can be increased. Our planned contributions include enhancing documentation for the authentication process by explaining token handling, rate limiting, and the sequence of checks in a clearer way, updating state.py and noxfile.py to document the risks of pickle, tightening retry splay logic, and replacing fragile assert statements with more robust error handling. We also aim to create a practical guide that helps users enable key security features that are not active by default so new users can configure the system more confidently. In addition, we intend to explore related open-source communities to identify other opportunities for contribution and to improve the clarity of token management documentation, which is currently difficult for newcomers to follow. Overall, the project is well organized and stable, with only a few areas that can benefit from clearer documentation and modest refinements.


### Team Reflection
We enjoyed using a hybrid approach of automated tools and manual inspection to analyze the Salt codebase. Farjad developed a secure coding mindset, appreciating automated tools while recognizing that manual analysis is needed to supplement their limitations. Joe found static analysis tools invaluable for complex codebases, emphasizing the need for a clear strategy and verifying meaningful findings. Alfawzan learned to scope code reviews effectively using CWE checklists and tools like Bandit, and confirmed the impact of findings manually. Tyler gained experience in manual code assessment, learning what personal coding practices to change and adopting the essential mindset and questions for secure development. John determined that manual review is necessary to catch subtle logical and architectural weaknesses that static analysis tools miss. The most valuable takeaway was realizing the effectiveness of this hybrid security approach combining automated and manual review to achieve comprehensive and accurate results.

### GitHub Repository
[CYBR8420_Team3_GitHub](https://github.com/smfarjad/CYBR8420_Team3/)

[CYBR8420_Team3_Project_Board](https://github.com/users/smfarjad/projects/3)

