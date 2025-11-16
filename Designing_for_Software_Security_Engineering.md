# Assignment Part 1: Threat Modeling









# Assignment Part 2: Observations

### Threat Mitigation and Identified Gaps

**Alfawzan**:



**Farjad**:
Some expected mitigations are already present: Salt is configured to use master–minion key-based authentication, basic artifact integrity checks via hashes in the CI pipeline, logging through system/Salt logs, and mostly HTTPS/TLS for repository and CI communication. When artifacts or checks fail, deployments generally fail closed, which matches the assumptions from our threat model.

However, I also observed several gaps:
- Salt Role-Based Access Control (external_auth, fine-grained permissions) and centralized SSO/MFA for admins are not fully configured.

- Logging is not centralized or audit-grade (no dedicated SIEM or append-only audit trail).

- TLS and certificate validation are not explicitly enforced and documented for all internal flows.

- The artifact repository is not deployed in a true HA (High Availability) configuration, and explicit rate/resource limits are missing.

- The Pre-flight Verification Gate and Salt Minions are not fully hardened (least-privilege accounts, sandboxing, module allow-lists).



**Tyler**: 



**Joe**:

SaltStack provides the building blocks for secure communication. However, its overall security posture is highly vulnerable due to a weak default security baseline. Core defenses such as TLS are optional and not enforced as the default security baseline. Additionally, many of Salt’s security features are optional and rely on administrators to enable them manually.  
 

Other security gaps: 

- No built-in rate limiting or DoS protection with known master 

- Insufficient input validation framework 

- No built-in SIEM integration 

- Requires extensive manual hardening 


**John**:





### Team Reflection:

**Alfawzan**:



**Farjad**:
This was my first time using a threat modeling tool. I was surprised to see how the Microsoft Threat Modeling Tool generated threats based on our DFD. These threats were similar to what I was  expecting in prior assignments. I also learned how trust boundaries, layered segmentation, and sanity checks contribute to improving the security of a system. The most useful takeaway from this assignment was developing a security mindset and understanding how multiple layers are important for improving the security of the system under consideration.



**Tyler**: 



**Joe**:




**John**:





# Progress & Contribution Planning

**Current Status:** This assignment gave us focused direction on the identified gaps, which we can now prioritize and address with the intent to make real contributions to the Salt codebase.

**Next Steps:** We plan to study these gaps in more detail and target a subset of them for pull requests to the SaltStack codebase. We will also consider the feasibility of each gap based on the effort required and the limited time available.


### GitHub Repository:
[CYBR8420_Team3_GitHub](https://github.com/smfarjad/CYBR8420_Team3/)
[CYBR8420_Team3_Project_Board](https://github.com/users/smfarjad/projects/3)

