# Assignment Part 1 - Assurance Case Development


### **1. Top-Level Claim 1** 
#### C1: Salt minimizes the risk of unauthorized administrative access.
#### Contributor: Joe Nguyen
#### Assurance Case Diagram:
![Claim 1](./assurance_cases/Claim_Joe.svg)
#### Usefulness of AI Prompt:
“You are a software security engineer, and you need to suggest some rebuttals for the top claim “Salt minimizes the risk of unauthorized administrative access”. With the rebuttals you find, also include some evidence that could eliminate reason for doubt.” 

This prompt was very useful in my opinion. It listed both rebuttals and evidence to eliminate doubt (even though AI provided very short/vague answers). However, AI did list ideas that I was able to build off of- definitely a great way to help frame the diagram. 


### **2. Top-Level Claim 2** 
#### C2: Sensitive data stored in Salt Stack pillars is protected from unauthorized access.
#### Contributor: Sheikh Muhammad Farjad
#### Assurance Case Diagram:
![Claim 2](./assurance_cases/Claim_Farjad.svg)
#### Usefulness of AI Prompt:
Since I was already preparing for the midterm, I made notes on the slides covering assurance case analysis. I uploaded the notes PDF to Gemini 2.5 Flash and provided it with the following prompt to refine the assurance cases:

“You are an expert software security engineer. Your job is to criticize and/or refine the assurance claims, their rebuttals, and the evidence through eliminative induction. Please use the attached pdf, which contains additional details and description. If you are ready, let me know and then I will start providing you with the assurance claims, rebuttals and their corresponding evidence.”



### **3. Top-Level Claim 3** 
#### C3: All production deployments apply content that is authentic and has verified provenance.
#### Contributor: Mohammed Alfawzan
#### Assurance Case Diagram:
![Claim 3](./assurance_cases/Claim_Alfawzan.svg)
#### Usefulness of AI Prompt:
I used the second one statement from canvas for validating my use cases: 

"You are an expert software security engineer. Your job is to suggest rebutting defeater for a given assurance claim using the concept of eliminative induction where support/assurance increases as reasons for doubt are eliminated. Here is an example claim for which rebutting defeaters are identified. 
Claim: The bulb will glow when switched on
Rebuttal 1: Unless switch not connected to light
Rebuttal 2: Unless no power
Rebuttal 3: Unless dead light bulb
Use this statement as a potential claim for analysis. Keep the rebuttals short and intuitive for including in a readable diagram."

### **4. Top-Level Claim 4** 
#### C4: Salt ensures secure communication between Master and Minion.
#### Contributor: Tyler McCoid
#### Assurance Case Diagram:
![Claim 4](./assurance_cases/Claim_Tyler.svg)
#### Usefulness of AI Prompt:
The main prompt that I used for claim refinment was as follows.

You are an expert software security engineer. Your job is to suggest corrections or improvements in the phrasing of assurance claims. Claims concern critical properties that are risk-related. High confidence is needed in their realization. A claim is always worded with a predicate. Avoid claims about the supporting method/techniques. <br /> Bad claim: "The system uses AES encryption." Why? Because it is not interesting; just the technology is just a means to an end, but does not provide assurance that it can actually keep the information confidential. Claim should be a reasonable goal (outcome). Good claim: “The system minimizes information disclosure during communication” <br /> Good Claim Checklist: 1. Includes an entity relevant to the argument, 2. a critical property of the entity, 3. a value for the property and related uncertainty. Use this statement as a potential claim for analysis. Explain why or why not this statement is a good claim. 
<br />""" 
<br />Claim here
<br />"""

### **5. Top-Level Claim 5** 
#### C5: Salt mitigates unauthorized administrative access
#### Contributor: John Winchester
#### Assurance Case Diagram:
![claim 5](./assurance_cases/Claim_John.svg)
#### Usefulness of AI Prompt:
These always have a bit of mixed feelings. I usualy get mixed results when telling the AI to pretend it's a role. It also seems to cost more tokens, but if it's some what passive it also gets more positive then negative. This kind of prompt also changes depeending on what engine you prompt as well. 

For this diagram I used the first prompt. 
The prompts below:
<details> 
Prompt 1: 
 You are an expert software security engineer. Your job is to suggest corrections or improvements in the phrasing of assurance claims. Claims concern critical properties that are risk-related. High confidence is needed in their realization. A claim is always worded with a predicate. Avoid claims about the supporting method/techniques. 
Bad claim: "The system uses AES encryption." Why? Because it is not interesting; just the technology is just a means to an end, but does not provide assurance that it can actually keep the information confidential. 
Claim should be a reasonable goal (outcome). Good claim: “The system minimizes information disclosure during communication”
Good Claim Checklist: 1. Includes an entity relevant to the argument, 2. a critical property of the entity, 3. a value for the property and related uncertainty. 
Use this statement as a potential claim for analysis. Explain why or why not this statement is a good claim. 
 
""" 
Canvas uses AES encryption
"""

</details>





# Assignment Part 2 - Identified Gap and Reflection


### Joe Nguyen
#### Alignment of Evidence and Identified Gap:
- **Evidence E1:** token_expire configuration logs: Salt does allow the configuration of token expiration times. The default setting time may be a bit too long and should be configured. Salt does not have detailed audit logs for token expiration configurations. Salt could implement a monitoring solution to generate and collect these logs to improve assurance.  

- **Evidence E2:** NTP Status Monitoring Report: Salt provides NTP management states that enforce NTP configurations, but it doesn’t look like Salt has a built-in NTP status monitoring report. Similarly to evidence 1, Salt could incorporate monitoring tools that could collect and report on the NTP status. 

- **Evidence E3:** TLS Certificate Logs: Based on Salt’s documentation, Salt doesn’t provide TLS certificate logs directly. However, Salt does provide TLS support and configuration options. When configured and monitored properly, users can provide the necessary evidence. 

- **Evidence E4:** Network security scan results: Just like any other OSS, Salt has had vulnerabilities that were later patched. This highlights the importance of regular network security scans. Salt does not have a built-in network security scanner but relies on external tools to scan for vulnerabilities. 

- **Evidence E5:** Compliance Audit Reports: Salt relies on external authentication providers; Salt would have to work directly with the external authentication providers to obtain compliance audit reports.  
#### Reflection:
 
This assignment helped me better understand how to evaluate and justify security claims using evidence. I also learned a lot from browsing Salt’s documentation and features. What I found most useful was using AI in the assurance diagram. With a good prompt- it could be a great tool to help brainstorm ideas.  

### Sheikh Muhammad Farjad
#### Alignment of Evidence and Identified Gap:

**Evidence either Available or Requiring Minimal Effort.** These items are generally available as static and standard artifacts within the Salt project repository and require primary manual review effort.

- **Evidence E2.1.1.1 Source code management (SCM) audit logs:** These logs are standard artifacts produced by version control systems used in Salt development. The effort lies in the manual review to confirm the logs demonstrate the automated checks (C2.1.1) are being enforced and effective.
- **Evidence E2.2.1.1 Salt master configuration (top.sls) review:** Configuration files are core components of the Salt project and are readily reviewable. The required effort is the manual review to systematically verify that the configuration enforces least-privilege scoping (C2.2.1).


**Evidence Requiring Additional Effort.** These items are not inherent to the source code and necessitate deployment, execution, or specialized tooling to generate.

- **Evidence E2.1.1.2 Pillar file content scan report:** Generating this report requires running a dedicated automated analysis tool specifically designed to scan the source code repository for sensitive plaintext data. This necessitates tool deployment, execution, and artifact generation, which is not a standard, inherent part of the code base.
- **Evidence E2.2.1.2 Results of access testing:** This is dynamic testing evidence. It requires setting up a deployed system and conducting dedicated security tests to verify the outcome (restricted access), necessitating system deployment, test execution, and documentation of outcomes, moving beyond static analysis.
- **Evidence E2.3.1.1 Secrets manager audit logs:** These are runtime operational artifacts. Their collection requires the system to be deployed and operated with specific, detailed logging enabled, and the relevant data extracted and analyzed.
- **Evidence E2.3.1.2 Vulnerability scan report for the external secrets management system:** This evidence supports the security of the third-party component (C2.3). It requires running specialized security assessments or vulnerability scans against that independent system, requiring external tool execution and expert security interpretation.




#### Reflection:
- **What did you learn from this assignment?** I learnt to develop and structure a formal assurance case, connecting high-level security goals to verifiable evidence using principles like eliminative induction. I reflected on how this specific set of rules (e.g., syntax and grammatical principles) contributes to the critical framing of assurance cases through eliminative induction. While this is helpful for assurance case development, it also provided me with the pointers to use this in real life for assessing claims.

- **What did you find most useful?** Prior to this assignment, I was not quite serious and cautious about using LLMs purposefully. This assignment gave me concrete pointers on how to use an LLM for refining the claims and other aspects of the assurance case, which must follow specific syntax and description rules.


### Tyler McCoid
#### Alignment of Evidence and Identified Gap:

**Evidence either Available or Requiring Minimal Effort.**
- **Evidence E1: Key rotation supported in code** Inside the documentation, key rotation is supported and is turned on by default. This key rotation happens daily.
- **Evidence E2: AES encryption logs** Inside the documentation, Salt states that it uses both RSA to send a public key, then uses AES for communication afterward. This can be checked by  
- **Evidence E3: Key acceptance configuration settings** Inside the documentation, Salt does not have auto-accept, which accepts any new minion without verification. The admin can set up a list of accepted characteristics in the autosign_grains_dir, for example, a uuid that will be automatically accepted. 

#### Reflection:
- From this assignment, I was able to understand the importance of creating an assurance case diagram. This allowed me to understand and prove to others that security vulnerabilities are covered by pointing to pieces of evidence that are implemented in the code and documentation. What I found most useful is learning the mindset that was needed to understand and create an assurance case diagram. This mindset will allow me to be able to systematically break apart an application to identify where there could be vulnerabilities and see if there is evidence to see if they are patched. 


### Mohammed Alfawzan
#### Alignment of Evidence and Identified Gap:
- **Evidence E1:** Gate run JID/log (SHA/signature check): Collect the JID and master/minion logs that show source_hash verification and the list of approved Git remotes; this proves the artifact and its origin for that deploy. 
Gap: add a small release manifest (pinned SHAs/signed tag) to bind the release to specific commits.


- **Evidence E2:** Negative test report (blocked unverified deploy): Trigger the pre-flight in fail-closed mode with a bad hash and archive the failed JID plus logs; this demonstrates the gate actually blocks tampered content.
Gap: an optional fleet-wide compliance check that records the gate settings (e.g., failhard) on all nodes.


- **Evidence E3:** Per-path gate-test report: Exercise each production entry path (CLI/orchestrate, salt-ssh, API) and save one JID per path as proof the gate is enforced everywhere. 
Gap: create a simple path registry file listing allowed entry paths and owners.


- **Evidence E4:** Automated discovery scan result: Run a lightweight discovery script that enumerates active entry paths and diffs them against the registry, with a CI job publishing the latest scan and gate-test artifact. 
Gap:  no automatic way to find active entry paths or keep the report current; add a small discovery script and a CI job to run it and publish the latest scan.


#### Reflection:

This assignment helped me turn vague security ideas into a clear assurance story. Writing an outcome focused claim made me think about what production must actually achieve, and the unless rebuttals pushed me to think like a skeptic and finish each branch with real evidence such as a job id log, a config snippet, or a short report. The most useful part was mapping our planned evidence to what Salt already provides versus what we must add, which exposed practical gaps like a release manifest and a path registry and gave me a concrete checklist for next steps.




### John Winchester
#### Alignment of Evidence and Identified Gap:
**Evidence either Available or Requiring Minimal Effort.**

**NOTE: Salt does not directly enforce commit signing or repository review It's heavily reliance on GitFS backends.**

- **Evidence E1:** Salt relies on GitFS for state management, which can integrate with Git repositories that enforce signed commits and tags. CI/CD pipelines can verify commit authenticity before deployment and log results.  

- **Evidence E2:** The Salt master configuration supports SSL verification and environment whitelisting to limit trusted Git remotes. Admins can review the master config file to confirm these options.  

- **Evidence E3:** Branch protection rules and CODEOWNERS files ensure multi-party review before changes are merged. These artifacts can be exported from repository settings or version control metadata.  

- **Evidence E4:** Continuous-integration workflows already include status check policies for testing and linting. Exporting the YAML definition or a successful run artifact provides proof of policy enforcement.  


- **Evidence E5:** GitHub and other hosting services maintain auditable logs of push, merge, and permission events. Downloading these logs demonstrates maintainer activity tracking.  

**Evidence Requiring Additional Effort.**
- **Evidence E6:** Webhooks must be configured to monitor critical repository changes such as branch protection updates or permission edits. Evidence includes a screenshot or export of webhook settings showing event types and destination endpoints.  

- **Evidence E7:** This evidence demonstrates that the alerting system successfully detects and records policy changes. Artifacts can include Slack notifications, SIEM logs, or GitHub alert exports showing triggered events. 



**Evidence either Available or Requiring Minimal Effort.**

**NOTE: Salt does not directly enforce commit signing or repository review It's heavily reliance on GitFS backends.**
- **Evidence E1: CI job log showing `git verify-commit` and pinned SHA**  
  Salt relies on GitFS for state management, which can integrate with Git repositories that enforce signed commits and tags. CI/CD pipelines can verify commit authenticity before deployment and log results.  

- **Evidence E2: `/etc/salt/master` GitFS configuration with `verify_ssl: True` and `env_whitelist`**  
  The Salt master configuration supports SSL verification and environment whitelisting to limit trusted Git remotes. Admins can review the master config file to confirm these options.  

- **Evidence E3: Branch-protection settings and CODEOWNERS file**  
  Branch protection rules and CODEOWNERS files ensure multi-party review before changes are merged. These artifacts can be exported from repository settings or version control metadata.  

- **Evidence E4: CI workflow YAML enforcing review gates**  
  Continuous-integration workflows already include status check policies for testing and linting. Exporting the YAML definition or a successful run artifact provides proof of policy enforcement.  


- **Evidence E5: Repository audit log CSV or JSON export**  
  GitHub and other hosting services maintain auditable logs of push, merge, and permission events. Downloading these logs demonstrates maintainer activity tracking.  

**Evidence Requiring Additional Effort.**
- **Evidence E6: Webhook configuration for real-time monitoring of repository events**  
  Webhooks must be configured to monitor critical repository changes such as branch protection updates or permission edits. Evidence includes a screenshot or export of webhook settings showing event types and destination endpoints.  

- **Evidence E7: Security alert report confirming detection of branch-rule or permission changes**  
  This evidence demonstrates that the alerting system successfully detects and records policy changes. Artifacts can include Slack notifications, SIEM logs, or GitHub alert exports showing triggered events.  

#### Reflection:
- **What did you learn from this assignment?**

I found out I need to scrutinize my work a lot more. This current work flow goes a lot more on github or other outside mechanisms. Salt does not directly enforce the commit signing or repository review. It ensures integrity through trusted GitFS backends.

# Progress & Contribution Planning

**Current Status:** This assignment was highly beneficial for identifying opportunities for open-source contributions through the eliminative induction process. We have enumerated multiple options for contributions; some of these require minimal effort, while others necessitate substantial effort.

**Next Steps:** Our next task is to prioritize the identified gaps. Following this prioritization, we will concentrate our efforts on addressing these items with the ultimate goal of contributing impactful changes to the official Salt repository.

### GitHub Repository:
[CYBR8420_Team3](https://github.com/smfarjad/CYBR8420_Team3/)
