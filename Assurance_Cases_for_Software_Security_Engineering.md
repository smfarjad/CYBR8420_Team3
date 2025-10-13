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
#### C2: 
#### Contributor: Sheikh Muhammad Farjad
#### Assurance Case Diagram:
![Claim 2](./assurance_cases/Claim_Farjad.svg)
#### Usefulness of AI Prompt:
Blah blah blah blah. 


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
E1- token_expire configuration logs 

Salt does allow the configuration of token expiration times. The default setting time may be a bit too long and should be configured. Salt does not have detailed audit logs for token expiration configurations. Salt could implement a monitoring solution to generate and collect these logs to improve assurance.  

E2- NTP Status Monitoring Report 

Salt provides NTP management states that enforce NTP configurations, but it doesn’t look like Salt has a built-in NTP status monitoring report. Similarly to evidence 1, Salt could incorporate monitoring tools that could collect and report on the NTP status. 

E3- TLS Certificate Logs 

Based on Salt’s documentation, Salt doesn’t provide TLS certificate logs directly. However, Salt does provide TLS support and configuration options. When configured and monitored properly, users can provide the necessary evidence. 

E4- Network security scan results  

Just like any other OSS, Salt has had vulnerabilities that were later patched. This highlights the importance of regular network security scans. Salt does not have a built-in network security scanner but relies on external tools to scan for vulnerabilities. 

E5- Compliance Audit Reports  

Salt relies on external authentication providers; Salt would have to work directly with the external authentication providers to obtain compliance audit reports.  
#### Reflection:
 
This assignment helped me better understand how to evaluate and justify security claims using evidence. I also learned a lot from browsing Salt’s documentation and features. What I found most useful was using AI in the assurance diagram. With a good prompt- it could be a great tool to help brainstorm ideas.  

### Sheikh Muhammad Farjad
#### Alignment of Evidence and Identified Gap:

#### Reflection:
- **What did you learn from this assignment?**
- **What did you find most useful?**


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
