# Assignment Part 1: Threat Modeling


https://htmlpreview.github.io/?https://github.com/smfarjad/CYBR8420_Team3/blob/DFD-Tyler/DFD/Salt%20DFD%20Report.htm


The Data Flow Diagram (DFD) generated a substantial list of 101 threats, which the team divided evenly, with one member (Farjad) handling an additional threat.

After each member drafted mitigations for their assigned threats within the DFD, the team initiated a cyclic review and update phase. This process involved sharing the updated DFD among members, allowing for efficient peer review to validate and refine each other's proposed mitigations.

The final, collaboratively reviewed DFD was then converted into an HTML report by one member (Tyler). This iterative approach, featuring distributed effort and a steady feedback loop, proved effective for achieving a thoroughly vetted and documented threat model. We relied on our Discord server for this fast review and update process.

# Assignment Part 2: Observations

### Threat Mitigation and Identified Gaps

**Alfawzan - (Number of assigned threats: 20)**

-Salt is strong at runtime with secure TLS communication and Token Validation, with strong activity logging, but plenty of gaps are still present. Certain portions seem inconsistent or very broad with other mechanisms not being present.

- The release gate does not require signed manifests or provenance and does not fail closed on verification errors.

- There is no allow list for trusted artifact sources or repository paths.

- Targeting and role-based access feel broad; minion keys are accepted without strong per-env/per-change validation.

- There are no canary or phased rollouts and no clearly tested rollback plan.

- Logs are centralized but not append-only or tamper-evident, and there is no alerting on risky events.

- Token database controls are unclear: least-privilege access, rotation, and short-lived token enforcement are not consistently applied.



**Farjad - (Number of assigned threats: 21)**

Some expected mitigations are already present: Salt is configured to use master–minion key-based authentication, basic artifact integrity checks via hashes in the CI pipeline, logging through system/Salt logs, and mostly HTTPS/TLS for repository and CI communication. When artifacts or checks fail, deployments generally fail closed, which matches the assumptions from our threat model.

However, I also observed several gaps:
- Salt Role-Based Access Control (external_auth, fine-grained permissions) and centralized SSO/MFA for admins are not fully configured.

- Logging is not centralized or audit-grade (no dedicated SIEM or append-only audit trail).

- TLS and certificate validation are not explicitly enforced and documented for all internal flows.

- The artifact repository is not deployed in a true HA (High Availability) configuration, and explicit rate/resource limits are missing.

- The Pre-flight Verification Gate and Salt Minions are not fully hardened (least-privilege accounts, sandboxing, module allow-lists).



**Tyler - (Number of assigned threats: 20)**

Many of the threats that I looked at were either mitigated completely or partially mitigated. The ones that were fully mitigated were the threats that went along with encrypted communication between systems with the use of AES. One of the main gaps that I noticed is that lots of the partial mitigations needed to be turned on by an administrator and are not on my default. Another gap that I noticed is that public channels broadcast to all minions and could lead to problems if mis-targeted jobs are sent. 


**Joe - (Number of assigned threats: 20)**

SaltStack provides the building blocks for secure communication. However, its overall security posture is highly vulnerable due to a weak default security baseline. Core defenses such as TLS are optional and not enforced as the default security baseline. Additionally, many of Salt’s security features are optional and rely on administrators to enable them manually.  
 

Other security gaps: 

- No built-in rate limiting or DoS protection with known master 

- Insufficient input validation framework 

- No built-in SIEM integration 

- Requires extensive manual hardening 


**John - (Number of assigned threats: 20)**

Much of the threats are partially mitigated with built in Salt mechanisms and priviledge settings. For applications like this, there's a lot of reliance on infrastructure, or firewall settings. There are quite a few partial mitigations due to mechanisms and configurations, but there's a heavy depandance on infrastructure to handle various other kinds of attacks. 

Summary of Findings
- Most threats related to *Tampering* and *Spoofing* were mitigated through Salt's ZeroMQ's authentication, signed job payloads, minion identity validation.
- Information disclosure threats were mitigated through TLS- based transport encryption and the secure job cache behavior
- Much of our Repudiation and Authorization threats are only partially mitigated, since Salt relies on external logging and OS level audits. 

Gaps
- Salt doesn't provide hardened privilege boundaries by default.
- Audit keys are not cryptographically protected in some cases.
- Keys stored on a master are not hardware backed.
- Token reuse and lifetime policies are configurable but not enforced strongly.
- Large reliance on proper configuration
- Heavy reliance on infrastructure 

AI Prompt used:
<details>
For the given DFD diagram apply STRIDE per Interaction. Focus on interactions that cross the threat boundary.
For each interaction, enumerate plausible spoofing, tampering, repudiation, information disclosure, denial of service, and elevation of privilege threats.
Propose mitigations that align with the architecture, not fight it. For each threat, suggest control options at the right layer, note tradeoffs, and highlight quick wins versus structural fixes. Where appropriate, add design guardrails that prevent entire classes of issues rather than patching symptoms.
</details>


### Team Reflection:

Working on this project, we learned how challenging yet rewarding it is to use threat modeling to break down complex system architectures into clear, actionable security insights. Each of us came away with different insights. Mohammed deepened his understanding of data flow diagrams (DFD), realizing that a simple mindset of "who sends what to whom" surfaces real risks at handoffs and wherever tokens cross a boundary. He found that assurance claims only matter when tied to evidence, like a cryptographic signature or an allow list decision. Farjad reflected on how trust boundaries, layered segmentation, and sanity checks contribute to improving system security, and he was surprised by how the Microsoft Threat Modeling Tool (MTMT) generated relevant threats based on the DFD. Tyler found the threat modeling tool impactful in pointing out possible threats and gained a more complete understanding of creating DFD diagrams, building on prior knowledge. Joe found the modeling tool the most useful and interesting, realizing how simply diagramming a system and seeing where trust boundaries exist makes it easier to visualize exposed areas and potential threats. John learned about the security-focused DFD style and, despite the initial learning curve, recognized the value of the MTMT from an engineering perspective, realizing how Defense in Depth methods make applications more robust. Overall, the most useful lesson was recognizing how forcing in a pre-flight verification gate and separating components like the identity provider and deployment agents was the most helpful part, as the missing controls, such as signed manifests and short-lived tokens, almost highlighted themselves for a practical to-do list.


# Progress & Contribution Planning

**Current Status:** This assignment gave us focused direction on the identified gaps, which we can now prioritize and address with the intent to make real contributions to the Salt codebase.

**Next Steps:** We plan to study these gaps in more detail and target a subset of them for pull requests to the SaltStack codebase. We will also consider the feasibility of each gap based on the effort required and the limited time available.


### GitHub Repository:
[CYBR8420_Team3_GitHub](https://github.com/smfarjad/CYBR8420_Team3/)

[CYBR8420_Team3_Project_Board](https://github.com/users/smfarjad/projects/3)

