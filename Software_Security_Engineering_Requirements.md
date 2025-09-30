# Assignment Part 1

## 1. Five Essential Interactions (Use/Misuse Cases)

### 1.1 Use Case 1 - Manage Pillars (Contributor: Sheikh Muhammad Farjad)

![Manage Pillars](./use_cases/Use-Misuse_Case-Farjad.svg)






**Derived Security Requirements:**
- **SR-01:** Blah blah blah
- **SR-02:** Blah blah blah


### 1.2 Use Case 2 - Your Use Case (Contributor: Joe Nguyen)



![Authentication/Authorization System](./use_cases/Use-MisuseJoe.svg)






**Derived Security Requirements:**
- **SR-03:**
- **SR-04:**



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

**Sheikh Muhammad Farjad** :

**Tyler McCoid** : With this assignment, I got to learn more about how to use the features of Draw.io for creating diagrams. With this specific assignment, I also learned the importance of how use and misuse cases can be used for understanding the security requirements that a system needs. With understanding how a system will be used and the possibilities of how a bad actor will try to use the system, one can derive what defenses need to be put in place.  

**Joe Nguyen**: 

**John Winchester**: I learned that there's quite a few different attack processes when dealing with changing a state file. This is so far pretty simplistic but it could end up looking quite complicated. Showing rounds in the loop shows the progression similar to our readings where one malicious attack may be nullified or mitigated for a new attack to present itself. Specific to Salt there's a bit more we could go into in terms of continuing this tree such as using Cryptographic signitures that could make a lot of this much more complicated for an attacker to pull off. 





# Assignment Part 2

### Sheikh Muhammad Farjad:


### Joe Nguyen:


### Mohammed Alfawzan: 


### Tyler McCoid:  
While reviewing the security-related documentation, I discovered that many of the security features are often left optional. During the installation process, there is no main page that talks about the security settings of Salt in the installation documentation. The page that talks about the security is listed in the Salt User Guide. A recommendation that I have is to also include the security features that are used at the end of the install guide to make sure that the users understand what features should be enabled to provide the best security. 


### John Winchester:



