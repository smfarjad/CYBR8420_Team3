# Assignment Part 1

## 1. Five Essential Interactions (Use/Misuse Cases)

### 1.1 Use Case 1 - Manage Pillars (Contributor: Sheikh Muhammad Farjad)

![Manage Pillars](./use_cases/Use-Misuse_Case-Farjad.svg)






**Derived Security Requirements:**
- **SR-01:** Blah blah blah
- **SR-02:** Blah blah blah


### 1.2 Use Case 2 - Your Use Case (Contributor: Joe Nguyen)







**Derived Security Requirements:**
- **SR-03:**
- **SR-04:**



### 1.3 Use Case 3 - Remote Deployment (Contributor: Mohammed Alfawzan)






**Derived Security Requirements:**
- **SR-05:** 
- **SR-06:**  



### 1.4 Use Case 4 - Your Use Case (Contributor: Tyler McCoid)






**Derived Security Requirements:**
- **SR-07:** 
- **SR-08:** 


### 1.5 Use Case 5 - distribute state file (Contributor: John Winchester)
![Distributed State Files Misuse Case](./use_cases/MisUseCasesV4greyovals.svg)





**Derived Security Requirements:**
- **SR-09:** All state file changes must undergo formal Review of State Changes before distribution.
- **SR-10:** Monitor/audit maintainer activity to detect compromise.  


**2. Team Reflection**

**Mohammed Alfawzan** : I learned that remote deploy isn’t just running a script it’s about who can deploy, what you trust, and how you prove it worked. The most useful part was the misuse→control loop: think like an attacker (unauthorized prod deploy, poisoned artifacts, fake checks) and then pin a concrete Salt control to it (eAuth/ACL, source_hash, tags, pillar.gpg, returners). That trace from threat → requirement → real feature made security feel practical, not theoretical.

**Sheikh Muhammad Farjad** :

**Tyler McCoid** :

**Joe Nguyen**: 

**John Winchester**: I learned that there's quite a few different attack processes when dealing with changing a state file. This is so far pretty simplistic but it could end up looking quite complicated. Showing rounds in the loop shows the progression similar to our readings where one malicious attack may be nullified or mitigated for a new attack to present itself. Specific to Salt there's a bit more we could go into in terms of continuing this tree such as using Cryptographic signitures that could make a lot of this much more complicated for an attacker to pull off. 





# Assignment Part 2

### Sheikh Muhammad Farjad:


### Joe Nguyen:


### Mohammed Alfawzan: 


### Tyler McCoid:


### John Winchester:



