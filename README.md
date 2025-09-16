## Open-Source Project: SaltStack Salt

## Repository and Team info

- **Team name:** Team 3 
- **Team members:** Joe Nguyen  John Winchester  Mohammed Alfawzan  Sheikh Muhammad Farjad  Tyler McCoid
- **GitHub repository link:** https://github.com/smfarjad/CYBR8420_Team3
- **Project board:** https://github.com/users/smfarjad/projects/3

---

## Project details

- **Name:** Salt (SaltStack / Salt Project) 
- **Repository:** https://github.com/saltstack/salt 
- **Description:**  
  Salt is an event-driven automation engine/framework, primarily used to manage configuration and orchestration of infrastructure at scale. It employs a master/minion architecture, has modules for states, execution, plugins, templating via Jinja, etc. 
- **Languages / platform:**  
  Mostly Python, shell, Powershell, NSIS, C#, Jinja, and others.  
- **Popularity / activity:**  
  ~14.8k stars, 5.5k forks; active contributions; many external users.

---

## Hypothetical Operational Environment

- **Environment type:** Enterprise / large cloud + on-premise hybrid infrastructure  
- **Users / stakeholders:** System administrators, DevOps engineers, security team, infrastructure team  
- **Scale:** Hundreds to thousands of managed nodes (servers, virtual machines, network devices)  
- **Security constraints:** Strong internal security policies, compliance (e.g. internal audits), encrypted communications, strict authorization controls, supply chain integrity, etc.  
- **Reliability & availability requirements:** Should have high uptime, ability to recover from network partitioning or node failures.  

---

## Systems Engineering View Diagram

*(Insert diagram here.)*


- **Environment of Operation:** Enterprise hybrid infrastructure with strict security, compliance requirements, internal and external network segmentation.

---

## Threats Perceived by Users

1. Unauthorized access to master or minion; key compromise.  
2. Eavesdropping or MITM attacks on the transport.  
3. Malicious state or execution modules (supply-chain or plugin).  
4. Misconfiguration leading to privilege escalation.  
5. DoS or overload from too many events or nodes.  
6. Configuration drift or divergence.  

---

## Security Features in Salt
![alt text](https://github.com/smfarjad/CYBR8420_Team3/blob/main/images/key-management.png)
- When a minion checks into the master it sends its public key to the master and the master checks if the key has been accepted.
- The minion will attempt to re-authenticate every 30 seconds until it’s key is accepted.
- If accepted then the master will accept the minion and allow it to accept commands.
- After the keys are sent to the master then the master will need to accept them. This acceptance is done with the salt-key command. Salt keys are used in the following ways:
- RSA keys are used for authentication
- An AES key is used for encryption
  - The AES key is changed every 24 hours by default, or when a minion is deleted.
 
### Other Security Features
- https://docs.saltproject.io/salt/user-guide/en/latest/topics/security.html#

---

## Motivation for Selecting This Project


---

## OSS Project Description

- **Contributors / Activity:** ~2,400+ contributors. Frequent commits, many open issues and pull requests.   
- **Languages used:** Primarily Python, with supporting code in Shell, PowerShell, etc.   
- **Platform / deployment:** Works on Linux, Windows, etc. Deployed inside data centers, cloud, hybrid. 
- **Documentation & support:** Official docs at docs.saltproject.io; security policy; contributing guidelines. 

---

## License & Contributor Agreements

- **License:** Apache 2.0 
- **Contributing Guidelines:** There is a `CONTRIBUTING.rst` in the repo; code of conduct; dependencies listed. :contentReference[oaicite:10]{index=10}  
- **Security Policy:** They have a `SECURITY.md` file; public security announcement channel. :contentReference[oaicite:11]{index=11}  

---

## Security History

- Known CVE for Saltstack Salt  https://nvd.nist.gov/vuln/detail/CVE-2020-11651  
- How the project handles security updates / patches?.  
- Examples of large-scale configuration mismanagement via Salt in past (if any)?.  

---

## Project Planning, Tracking

- **Task breakdown:** Who does what (diagram creation, threat research, module internals, etc.)  
- **Milestones:** e.g. finish diagram, finish threats/features section, finish license history, compile reflections, etc.  


