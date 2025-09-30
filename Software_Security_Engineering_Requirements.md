# Assignment Part 1

## 1. Five Essential Interactions (Use/Misuse Cases)

### 1.1 Use Case 1 - Manage Pillars (Contributor: Sheikh Muhammad Farjad)

![Manage Pillars](./use_cases/Use-Misuse_Case_Farjad.svg)


**Derived Security Requirements:**
- **SR-01:** All sensitive pillar data shall be stored only as encrypted blobs or as references to an approved secrets backend. The system shall reject any attempt to save plaintext secrets in repositories, caches, backups, or the Manage Pillar UI.
- **SR-02:** Pillar data shall be encrypted at rest and in transit using modern cryptography such as AEAD ciphers like AES-256-GCM or XChaCha20-Poly1305 for storage and TLS 1.2 or 1.3 with PFS via ECDHE for distribution. Weak or legacy options shall be disabled and keys shall be generated with a CSPRNG and stored in a KMS or HSM.



### 1.2 Use Case 2 - Your Use Case (Contributor: Joe Nguyen)



![Authentication/Authorization System](./use_cases/Use-MisuseJoe.svg)






**Derived Security Requirements:**
- **SR-03:** One important component of Salt is their authorization/authentication system. Salt is a bit unique because they use an external authorization system. Once a system administrator is authenticated, a token is sent to Salt to be validated. This validation step can be threatened by replay attacks. RSA Key signing verifies the master's identity and message integrity. Signatures let clients detect forged/tampered replies- signatures with the assistance of short-lived tokens/timestamps help prevent replay attacks. 
- **SR-04:** HTTPS/TLS encryption and HSTS provide encrypted and authenticated transport so attackers can't eavesdrop or tamper. HSTS and strict cert verification can help prevent TLS stripping attacks.
- Salt provides the right primitive security tools (RSA key signing, short-lived tokens, timestamps, TLS, etc.) to prevent replay and MITM attacks. However, these protections are opt-in/have risky defaults. For example: on their website, they mention that the default time for a token to expire was 43200 seconds or 12 hours. Salt can be safe, but only if system administrators configure it correctly (enable signing, enforce TLS, shorten token lifetimes, etc).



### 1.3 Use Case 3 - Remote Deployment (Contributor: Mohammed Alfawzan)






**Derived Security Requirements:**
- **SR-05:** 
- **SR-06:**  



### 1.4 Use Case 4 - Minion Monitoring (Contributor: Tyler McCoid)

![Minion Monitoring](./use_cases/Use-Misuse_Case.svg)




**Derived Security Requirements:**
- **SR-07:** The system shall use short-lived authentication to prevent bad actors from impersonating minions
- **SR-08:** Once a Minion is authenticated, the system shall make a secure channel with encrypted communication between the two.


### 1.5 Use Case 5 - distribute state file (Contributor: John Winchester)
![Distributed State Files Misuse Case](./use_cases/MisUseCasesV4greyovals.svg)





**Derived Security Requirements:**
- **SR-09:** All state file changes must undergo formal Review of State Changes before distribution.
- **SR-10:** Monitor/audit maintainer activity to detect compromise.  


**2. Team Reflection**

**Mohammed Alfawzan** : I learned that remote deploy isn’t just running a script it’s about who can deploy, what you trust, and how you prove it worked. The most useful part was the misuse→control loop: think like an attacker (unauthorized prod deploy, poisoned artifacts, fake checks) and then pin a concrete Salt control to it (eAuth/ACL, source_hash, tags, pillar.gpg, returners). That trace from threat → requirement → real feature made security feel practical, not theoretical.

**Sheikh Muhammad Farjad** : This assignment helped me in multiple dimensions. I learned how misuse-case analysis can lead directly to clear security requirements. I also practiced the grammar of writing requirements, especially using “shall” to state what the system must do. For collaboration, we used Git heavily and saw both its strengths and its limits. Pairing Git with an informal channel such as Discord proved more effective than using Git alone.

**Tyler McCoid** : With this assignment, I got to learn more about how to use the features of Draw.io for creating diagrams. With this specific assignment, I also learned the importance of how use and misuse cases can be used for understanding the security requirements that a system needs. With understanding how a system will be used and the possibilities of how a bad actor will try to use the system, one can derive what defenses need to be put in place.  

**Joe Nguyen**: 

This project allowed me to effectively use Draw.io. At first, I did struggle a lot when it came to moving things around and adding what I wanted, but after using the tool for a few hours, you get used to the application. Working through the diagrams also helped me better understand how misuse cases connect to system requirements and defenses. Making the diagrams not only improved my technical skills but also helped my ability to think critically about system requirements.


**John Winchester**: I learned that there's quite a few different attack processes when dealing with changing a state file. This is so far pretty simplistic but it could end up looking quite complicated. Showing rounds in the loop shows the progression similar to our readings where one malicious attack may be nullified or mitigated for a new attack to present itself. Specific to Salt there's a bit more we could go into in terms of continuing this tree such as using Cryptographic signitures that could make a lot of this much more complicated for an attacker to pull off. 





# Assignment Part 2

### Sheikh Muhammad Farjad:
While user documentation for Salt is detailed, partly due to the support from VMware, the security documentation and features have gaps that likely require community contributions. For example, I was surprised to learn there is no built-in at-rest encryption mechanism for pillar data. In practice, many teams use third-party utilities (e.g., [HashiCorp Vault](https://www.hashicorp.com/en/products/vault)) to encrypt pillar data. Otherwise, executing `pillar.items` (see [modules.pillar](https://docs.saltproject.io/en/3006/ref/modules/all/salt.modules.pillar.html)) reveals all pillar content in plaintext. This was especially surprising for a well-supported open-source tool like Salt.

### Joe Nguyen:
Salt’s security-related configurations are often optional, hidden in subsections, or left to the system administrator’s discretion. Salt could benefit from adding a “What to do after installation” checklist. This checklist could include recommended defaults, change to short-lived tokens, enable logging, disable auto-accept keys, etc. Based on Salt’s website, the installation process is pretty straightforward and simple to follow. However, it might be in Salt’s best interest to add some sort of “Secure Installing” section because security hardening is not part of the main installation process- it is another subsection that you must find on their website. The installation process is beginner friendly, but the security aspect of installing Salt is buried in detail.

### Mohammed Alfawzan: 


### Tyler McCoid:  
While reviewing the security-related documentation, I discovered that many of the security features are often left optional. During the installation process, there is no main page that talks about the security settings of Salt in the installation documentation. The page that talks about the security is listed in the Salt User Guide. A recommendation that I have is to also include the security features that are used at the end of the install guide to make sure that the users understand what features should be enabled to provide the best security. 


### John Winchester:



