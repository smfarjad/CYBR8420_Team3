# Assignment Part 1 - Assurance Case Development


### **1. Top-Level Claim 1** 
#### C1: Salt minimizes the risk of unauthorized administrative access 
#### Contributor: Joe Nguyen
#### Assurance Case Diagram:
![Claim 1](./images/AssuranceDiagramJoe.svg)
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
#### C3: 
#### Contributor: 
#### Assurance Case Diagram:

#### Usefulness of AI Prompt:
Blah blah blah blah. 

### **4. Top-Level Claim 4** 
#### C4: 
#### Contributor:
#### Assurance Case Diagram:

#### Usefulness of AI Prompt:
Blah blah blah blah. 


### **5. Top-Level Claim 5** 
#### C5: 
#### Contributor:
#### Assurance Case Diagram:

#### Usefulness of AI Prompt:
Blah blah blah blah. 


### **1. Top-Level Claim 1** 
#### C1: 
#### Contributor: Sheikh Muhammad Farjad
#### Assurance Case Diagram:

#### Usefulness of AI Prompt:
Blah blah blah blah. 


# Assignment Part 2 - Identified Gap and Reflection


### Joe Nguyen
#### Alignment of Evidence and Identified Gap:
- E1 - token_expire configuration logs: Salt does allow the configuration of token expiration times. The default setting time may be a bit too long and should be configured. Salt does not have detailed audit logs for token expiration configurations. Salt could implement a monitoring solution to generate and collect these logs to improve assurance.  

- E2 - NTP Status Monitoring Report: Salt provides NTP management states that enforce NTP configurations, but it doesn’t look like Salt has a built-in NTP status monitoring report. Similarly to evidence 1, Salt could incorporate monitoring tools that could collect and report on the NTP status. 

- E3 - TLS Certificate Logs: Based on Salt’s documentation, Salt doesn’t provide TLS certificate logs directly. However, Salt does provide TLS support and configuration options. When configured and monitored properly, users can provide the necessary evidence. 

- E4 - Network security scan results: Just like any other OSS, Salt has had vulnerabilities that were later patched. This highlights the importance of regular network security scans. Salt does not have a built-in network security scanner but relies on external tools to scan for vulnerabilities. 

- E5 - Compliance Audit Reports: Salt relies on external authentication providers; Salt would have to work directly with the external authentication providers to obtain compliance audit reports.  
#### Reflection:
 
This assignment helped me better understand how to evaluate and justify security claims using evidence. I also learned a lot from browsing Salt’s documentation and features. What I found most useful was using AI in the assurance diagram. With a good prompt- it could be a great tool to help brainstorm ideas.  

### Sheikh Muhammad Farjad
#### Alignment of Evidence and Identified Gap:

**Evidence either Available or Requiring Minimal Effort.** These items are generally available as static and standard artifacts within the Salt project repository and require primary manual review effort.

- **E1.1.1.1 Source code management (SCM) audit logs:** These logs are standard artifacts produced by version control systems used in Salt development. The effort lies in the manual review to confirm the logs demonstrate the automated checks (C1.1.1) are being enforced and effective.
- **E1.2.1.1 Salt master configuration (top.sls) review:** Configuration files are core components of the Salt project and are readily reviewable. The required effort is the manual review to systematically verify that the configuration enforces least-privilege scoping (C1.2.1).


**Evidence Requiring Additional Effort.** These items are not inherent to the source code and necessitate deployment, execution, or specialized tooling to generate.

- **E1.1.1.2 Pillar file content scan report:** Generating this report requires running a dedicated automated analysis tool specifically designed to scan the source code repository for sensitive plaintext data. This necessitates tool deployment, execution, and artifact generation, which is not a standard, inherent part of the code base.
- **E1.2.1.2 Results of access testing:** This is dynamic testing evidence. It requires setting up a deployed system and conducting dedicated security tests to verify the outcome (restricted access), necessitating system deployment, test execution, and documentation of outcomes, moving beyond static analysis.
- **E1.3.1.1 Secrets manager audit logs:** These are runtime operational artifacts. Their collection requires the system to be deployed and operated with specific, detailed logging enabled, and the relevant data extracted and analyzed.
- **E1.3.1.2 Vulnerability scan report for the external secrets management system:** This evidence supports the security of the third-party component (C1.3). It requires running specialized security assessments or vulnerability scans against that independent system, requiring external tool execution and expert security interpretation.




#### Reflection:
- **What did you learn from this assignment?** I learnt to develop and structure a formal assurance case, connecting high-level security goals to verifiable evidence using principles like eliminative induction. I reflected on how this specific set of rules (e.g., syntax and grammatical principles) contributes to the critical framing of assurance cases through eliminative induction. While this is helpful for assurance case development, it also provided me with the pointers to use this in real life for assessing claims.

- **What did you find most useful?** Prior to this assignment, I was not quite serious and cautious about using LLMs purposefully. This assignment gave me concrete pointers on how to use an LLM for refining the claims and other aspects of the assurance case, which must follow specific syntax and description rules.


### Tyler McCoid
#### Alignment of Evidence and Identified Gap:

#### Reflection:
- **What did you learn from this assignment?**
- **What did you find most useful?**


### Mohammed Alfawzan
#### Alignment of Evidence and Identified Gap:

#### Reflection:
- **What did you learn from this assignment?**
- **What did you find most useful?**



### John Winchester
#### Alignment of Evidence and Identified Gap:

#### Reflection:
- **What did you learn from this assignment?**
- **What did you find most useful?**


### GitHub Repository:
[CYBR8420_Team3](https://github.com/smfarjad/CYBR8420_Team3/)

