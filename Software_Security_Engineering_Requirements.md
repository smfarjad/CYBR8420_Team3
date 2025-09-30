# Assignment Part 1

## 1. Five Essential Interactions (Use/Misuse Cases)

### 1.1 Use Case 1 - Deploy Minion (Contributor: Sheikh Muhammad Farjad)

![Manage Pillars](./use_cases/Use-Misuse_Case_Farjad.svg)

*Note: Use Case 1 is different from Use Case 3 because it focuses on deploying minion with the misuse case analysis targeting the pillar management.

**Derived Security Requirements:**
- **SR-01:** All sensitive pillar data shall be stored only as encrypted blobs or as references to an approved secrets backend. The system shall reject any attempt to save plaintext secrets in repositories, caches, backups, or the Manage Pillar UI.
- **SR-02:** Pillar data shall be encrypted at rest and in transit using modern cryptography such as AEAD ciphers like AES-256-GCM or XChaCha20-Poly1305 for storage and TLS 1.2 or 1.3 with PFS via ECDHE for distribution. Weak or legacy options shall be disabled and keys shall be generated with a CSPRNG and stored in a KMS or HSM.

While Salt provides encryption, it is limited to communication channels involving the admin, master, and minion as endpoints. 



### 1.2 Use Case 2 - Your Use Case (Contributor: Joe Nguyen)



![Authentication/Authorization System](./use_cases/Use-MisuseJoe.svg)




**Derived Security Requirements:**
- **SR-03:** One important component of Salt is their authorization/authentication system. Salt is a bit unique because they use an external authorization system. Once a system administrator is authenticated, a token is sent to Salt to be validated. This validation step can be threatened by replay attacks. RSA Key signing verifies the master's identity and message integrity. Signatures let clients detect forged/tampered replies- signatures with the assistance of short-lived tokens/timestamps help prevent replay attacks. 
- **SR-04:** HTTPS/TLS encryption and HSTS provide encrypted and authenticated transport so attackers can't eavesdrop or tamper. HSTS and strict cert verification can help prevent TLS stripping attacks.

Salt provides the right primitive security tools (RSA key signing, short-lived tokens, timestamps, TLS, etc.) to prevent replay and MITM attacks. However, these protections are opt-in/have risky defaults. For example: on their website, they mention that the default time for a token to expire was 43200 seconds or 12 hours. Salt can be safe, but only if system administrators configure it correctly (enable signing, enforce TLS, shorten token lifetimes, etc).



### 1.3 Use Case 3 - Remote Deployment (Contributor: Mohammed Alfawzan)

![Remote Deployment (Misuse) — alfawzanxd](<./use_cases/Remote_deployment by Alfawzan .drawio.svg>)

![Remote Deployment](./use_cases/Remote_deployment%20by%20Alfawzan%20.drawio.svg)



**Derived Security Requirements:**
- **SR-05:** Artifact Encryption & Integrity Verification All artifacts and configuration pillars staged to targets must be stored encrypted at rest (via Salt’s GPG renderer or Vault integration) and verified with cryptographic digests/signatures at deployment time. Rationale: Prevents Artifact Poisoning by ensuring only authentic, untampered artifacts are applied
 
- **SR-06:**  Deployment Verification & Rollback Trigger Every remote deployment must be followed by automated verification checks (service health, integrity tests). If verification fails, the system must automatically initiate Rollback & Remediation to the last-known-good state. Rationale: Prevents Unauthorized/Unstable Production Deployment from persisting by detecting issues immediately and restoring stability.



### 1.4 Use Case 4 - Minion Monitoring (Contributor: Tyler McCoid)

![Minion Monitoring](./use_cases/Use-Misuse_Case_Tyler.drawio.svg)



**Derived Security Requirements:**
- **SR-07:** The system shall use short-lived authentication to prevent bad actors from impersonating minions
- **SR-08:** Once a Minion is authenticated, the system shall make a secure channel with encrypted communication between the two.


### 1.5 Use Case 5 - distribute state file (Contributor: John Winchester)
![Distributed State Files Misuse Case](./use_cases/MisUseCasesV4greyovals.svg)





**Derived Security Requirements:**
- **SR-09:** All state file changes must undergo formal Review of State Changes before distribution.
- **SR-10:** Monitor/audit maintainer activity to detect compromise.  



## 2. Team Reflection

As a team, we successfully navigated the challenges of a large open-source project like Salt, learning to transform complex documentation into clear, actionable content, which we used to elicit security requirements via misuse case analysis. **Mohammed** learned that remote deployment security extends beyond simple scripts, focusing on trust, proof, and the practical misuse-to-control loop (eAuth/ACL, source_hash, etc.) to derive concrete security features. **Farjad** recognized how misuse-case analysis directly leads to clear security requirements written with explicit grammar (e.g., using “shall”) and found that pairing heavy Git use with informal communication channels was essential for effective collaboration. **Tyler** gained proficiency with draw.io and confirmed the critical importance of use and misuse cases for defining necessary system defenses against malicious actors. **Joe** also became proficient with draw.io, realizing how visualizing these diagrams strengthens critical thinking about connecting misuse scenarios to firm system requirements. **John** explored the nuances of state file attack processes, observing the iterative nature of attack and defense and the critical role of cryptographic signatures in complicating attacker efforts. In summary, our most valuable lesson was how merging technical analysis with practical tools like draw.io and supplementing formal Git processes with steady, open communication ensured we stayed organized and made continuous progress.





# Assignment Part 2
For Part 2, we decided to explore the project individually, so that we can share our insights with each other. Our individual findings and insights are discussed as follows.

### Sheikh Muhammad Farjad:
While user documentation for Salt is detailed, partly due to the support from VMware, the security documentation and features have gaps that likely require community contributions. For example, I was surprised to learn there is no built-in at-rest encryption mechanism for pillar data. In practice, many teams use third-party utilities (e.g., [HashiCorp Vault](https://www.hashicorp.com/en/products/vault)) to encrypt pillar data. Otherwise, executing `pillar.items` (see [modules.pillar](https://docs.saltproject.io/en/3006/ref/modules/all/salt.modules.pillar.html)) reveals all pillar content in plaintext. This was especially surprising for a well-supported open-source tool like Salt. It also does not provide an explicit recommendation on the integration of third-party security solutions.

### Joe Nguyen:
Salt’s security-related configurations are often optional, hidden in subsections, or left to the system administrator’s discretion. Salt could benefit from adding a “What to do after installation” checklist. This checklist could include recommended defaults, change to short-lived tokens, enable logging, disable auto-accept keys, etc. Based on Salt’s website, the installation process is pretty straightforward and simple to follow. However, it might be in Salt’s best interest to add some sort of “Secure Installing” section because security hardening is not part of the main installation process- it is another subsection that you must find on their website. The installation process is beginner friendly, but the security aspect of installing Salt is buried in detail.

### Mohammed Alfawzan: 


### Tyler McCoid:  
While reviewing the security-related documentation, I discovered that many of the security features are often left optional. During the installation process, there is no main page that talks about the security settings of Salt in the installation documentation. The page that talks about the security is listed in the Salt User Guide. A recommendation that I have is to also include the security features that are used at the end of the install guide to make sure that the users understand what features should be enabled to provide the best security. 


### John Winchester:


# Progress & Contribution Planning

### Current Status: 
We are analyzing all derived security requirements and individual reflections from Part 2 of the assignment.

### Next Step: 
Our immediate task is to prioritize a selection of security requirements and the identified gap from Part 2. This will allow us to narrow our focus to specific, high-impact areas of the Salt codebase, with the goal of producing actionable contributions to the original repository.

