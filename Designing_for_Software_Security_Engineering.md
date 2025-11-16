# Assignment Part 1: Threat Modeling









# Assignment Part 2: Observations

### Threat Mitigation and Identified Gaps

**Alfawzan**:

- Mitigation review and gaps: Our Salt based remote deployment looks solid on the runtime side: the Salt Master talks to the external identity provider over TLS, checks tokens against the token database, and writes activity logs. The weak spots are mostly before production. We do not consistently verify a signed release manifest or provenance, the gate does not clearly fail closed on any verification error, and there is no clear allow list for approved artifact sources or paths. On production safety we accept minion keys, but targeting and role based access control feel broad, and we do not have canary or phased rollouts or a simple rollback plan. Logs are centralized but not tamper evident and there is no alerting on risky events. The token database works, but least privilege access, rotation, and short lived tokens are not clearly enforced. Those are the main gaps to close.

- The release gate does not require signed manifests or provenance and does not fail closed on verification errors.

- There is no allow list for trusted artifact sources or repository paths.

- Targeting and role-based access feel broad; minion keys are accepted without strong per-env/per-change validation.

- There are no canary or phased rollouts and no clearly tested rollback plan.

- Logs are centralized but not append-only or tamper-evident, and there is no alerting on risky events.

- Token database controls are unclear: least-privilege access, rotation, and short-lived token enforcement are not consistently applied.



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
What I learned: Drawing the data flow diagram made me think in terms of who sends what to whom across which boundary. That simple mindset surfaced the real risks at the handoff from the build and release pipeline to production and wherever tokens or admin commands cross a boundary. It also showed me how assurance claims only matter when they are tied to evidence, like a cryptographic signature check, an allow list decision, or a log that proves something happened.

What I found most useful: Forcing in a pre flight verification gate and separating the identity provider, the token database, and the deployment agents was the most helpful part. Once they were distinct boxes, the missing controls almost highlighted themselves, such as signed manifests, short lived tokens, canary and rollback, and tamper evident logging. The result is a short, practical to do list that hardens what we already have without a full redesign.

AI promt used: For the given DFD diagram apply STRIDE per Interaction. Focus on interactions that cross the threat boundary.
For each interaction, enumerate plausible spoofing, tampering, repudiation, information disclosure, denial of service, and elevation of privilege threats.
Propose mitigations that align with the architecture, not fight it. For each threat, suggest control options at the right layer, note tradeoffs, and highlight quick wins versus structural fixes. Where appropriate, add design guardrails that prevent entire classes of issues rather than patching symptoms.


**Farjad**:
This was my first time using a threat modeling tool. I was surprised to see how the Microsoft Threat Modeling Tool generated threats based on our DFD. These threats were similar to what I was  expecting in prior assignments. I also learned how trust boundaries, layered segmentation, and sanity checks contribute to improving the security of a system. The most useful takeaway from this assignment was developing a security mindset and understanding how multiple layers are important for improving the security of the system under consideration.



**Tyler**: 



**Joe**:

I found the modeling tool to be the most useful and most interesting. It was surprising how simply diagramming a system can surface a variety of threats. I learned a lot from making a data flow diagram. It helped me see how information moves within a system and where trust boundaries exist. Once the diagram was finished, it became much easier to visualize which parts of the system were most exposed and how different threats could occur.  



**John**:





# Progress & Contribution Planning

**Current Status:** This assignment gave us focused direction on the identified gaps, which we can now prioritize and address with the intent to make real contributions to the Salt codebase.

**Next Steps:** We plan to study these gaps in more detail and target a subset of them for pull requests to the SaltStack codebase. We will also consider the feasibility of each gap based on the effort required and the limited time available.


### GitHub Repository:
[CYBR8420_Team3_GitHub](https://github.com/smfarjad/CYBR8420_Team3/)

[CYBR8420_Team3_Project_Board](https://github.com/users/smfarjad/projects/3)

