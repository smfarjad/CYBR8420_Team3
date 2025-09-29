# Assignment Part 1

## 1. Five Essential Interactions (Use/Misuse Cases)

### 1.1 Use Case 1 - Manage Pillars (Contributor: Sheikh Muhammad Farjad)

![Manage Pillars](./use_cases/Use-Misuse_Case-Farjad.svg)






**Derived Security Requirements:**
- **SR-01:** Blah blah blah
- **SR-02:** Blah blah blah


### 1.2 Use Case 2 - Authentication/Authorization System (Contributor: Joe Nguyen)

![Authentication/Authorization System](./use_cases/FinalDiagramJoe.svg)





**Derived Security Requirements:**
- **SR-03:** One important component of Salt is their authorization/authentication system. Salt is a bit unique because they use an external authorization system. Once a system administrator is authenticated, a token is sent to Salt to be validated. This validation step can be threatened by replay attacks. RSA Key signing verifies the master's identity and message integrity. Signatures let clients detect forged/tampered replies- signatures with the assistance of short-lived tokens/timestamps help prevent replay attacks. 
- **SR-04:** HTTPS/TLS encryption and HSTS provide encrypted and authenticated transport so attackers can't eavesdrop or tamper. HSTS and strict cert verification can help prevent TLS stripping attacks. 
- Salt provides the right primitive security tools (RSA key signing, short-lived tokens, timestamps, TLS, etc.) to prevent replay and MITM attacks. However, these protections are opt-in/have risky defaults. For example: on their website, they mention that the default time for a token to expire was 43200 seconds or 12 hours. Salt can be safe, but only if system administrators configure it correctly (enable signing, enforce TLS, shorten token lifetimes, etc).


### 1.3 Use Case 3 - Remote Deployment (Contributor: Mohammed Alfawzan)

![Remote Deployment](./use_cases/Remote_deployment.svg)






**Derived Security Requirements:**
- **SR-05:**  Artifact Encryption & Integrity Verification
All artifacts and configuration pillars staged to targets must be stored encrypted at rest (via Salt’s GPG renderer or Vault integration) and verified with cryptographic digests/signatures at deployment time.
Rationale: Prevents Artifact Poisoning by ensuring only authentic, untampered artifacts are applied
- **SR-06:**  Deployment Verification & Rollback Trigger
Every remote deployment must be followed by automated verification checks (service health, integrity tests). If verification fails, the system must automatically initiate Rollback & Remediation to the last-known-good state.
Rationale: Prevents Unauthorized/Unstable Production Deployment from persisting by detecting issues immediately and restoring stability.




### 1.4 Use Case 4 - Your Use Case (Contributor: Tyler McCoid)






**Derived Security Requirements:**
- **SR-07:** 
- **SR-08:** 


### 1.5 Use Case 5 - Your Use Case (Contributor: John Winchester)






**Derived Security Requirements:**
- **SR-09:** 
- **SR-10:** 


**2. Team Reflection**

**Mohammed Alfawzan**


**Sheikh Muhammad Farjad**


**Tyler McCoid**


**Joe Nguyen**


This project allowed me to effectively use Draw.io. At first, I did struggle a lot when it came to moving things around and adding what I wanted, but after using the tool for a few hours, you get used to the application. Working through the diagrams also helped me better understand how misuse cases connect to system requirements and defenses. Making the diagrams not only improved my technical skills but also helped my ability to think critically about system requirements.  


**John Winchester**







# Assignment Part 2

### Sheikh Muhammad Farjad:


### Joe Nguyen:

Salt’s security-related configurations are often optional, hidden in subsections, or left to the system administrator’s discretion. Salt could benefit from adding a “What to do after installation” checklist. This checklist could include recommended defaults, change to short-lived tokens, enable logging, disable auto-accept keys, etc. Based on Salt’s website, the installation process is pretty straightforward and simple to follow. However, it might be in Salt’s best interest to add some sort of “Secure Installing” section because security hardening is not part of the main installation process- it is another subsection that you must find on their website. The installation process is beginner friendly, but the security aspect of installing Salt is buried in detail.   

### Mohammed Alfawzan:


### Tyler McCoid:


### John Winchester:



