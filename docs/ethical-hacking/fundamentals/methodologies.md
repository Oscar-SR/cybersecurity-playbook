# Methodologies

To perform a penetration test, it is necessary to follow a methodology. This ensures that no attack vector is overlooked and that the work can be validated and recognized by other professionals. It is considered good practice to state which methodology has been followed when conducting a penetration test, as it facilitates future re-tests and provides overall consistency to the final results.

Below is an overview of the most widely used methodologies in the information security industry, developed through collaboration among professionals from different countries.

## OSSTMM

The OSSTMM standard (Open Source Security Testing Methodology) is one of the most widely recognized standards in the industry, providing a scientific methodology for network penetration testing and vulnerability assessment. This methodology is **based on the tester’s in-depth knowledge and experience**, as well as on human intelligence to interpret the identified vulnerabilities and their potential impact within the network.

## OWASP

For everything related to **application security**, the Open Web Application Security Project (OWASP) is the most widely recognized standard in the cybersecurity industry. This methodology, driven by a highly skilled community that stays up to date with the latest technologies, has helped countless organizations mitigate application vulnerabilities.

## PTES

PTES (Penetration Testing Execution Standard) highlights the **most recommended approach for structuring a penetration test**. This standard guides professionals through the various stages of a penetration test, including initial communication, information gathering, and threat modeling phases.

### Pre-engagement interactions

This phase is usually presented as commercial proposals and customized for the client. It defines the preparation of the test and the activities that must be carried out before the actual penetration test. It specifies what should be analyzed, how, and when. To facilitate this, it is common to provide the client with questionnaires that they must complete.

### Intelligence gathering

Information gathering is the first step and the foundation for a successful penetration test. This phase is crucial and should not be rushed, as the more information we have, the higher the chances of success in our pentest. The purpose of collecting all this information is to understand how the application or system works in order to identify security weaknesses that can be addressed.

There are two types of information gathering:

- **Pasive information gathering**: This method can be used before active information gathering, as it is less invasive. Only publicly available information about the target is used, and all possible data is collected without establishing direct contact between the pentester and the target. The most relevant information includes IP address ranges, email addresses, external infrastructure profile, technologies in use, remote access methods, applications in use, IDS/IPS systems in place, and document metadata.

- **Active information gathering**: In this type of approach, greater preparation is required from the pentester, as it leaves traces that may trigger alerts on the target systems. With this method, the target organization may become aware of the ongoing process, since there is active engagement with the target. During this phase, information is obtained about open ports, running services, application versions, operating system versions, and more.

### Threat modeling

Threat modeling involves determining and defining the client’s business and analyzing which parts of the business may be most attractive to an attacker. These assets are the ones that should be evaluated at the business level, not at the technical level. The main objective of this phase is to enable auditors to accurately emulate real-world attacks, by “putting themselves in the attackers’ shoes.”

### Vulnerability analysis

During vulnerability analysis, we look for weaknesses in the infrastructure, network, systems, and applications, which can later be exploited and leveraged to achieve our objective.

### Exploitation

Once the vulnerabilities have been identified, the next step is to classify them and determine how they can be exploited. Ideally, the attack should be precise, with minimal impact on the systems.

This is the phase where the **auditor’s knowledge and experience play a major role**. It is the most interesting part of a penetration test and the stage where skills can truly be demonstrated.

Both custom and third‑party exploits may be used, systems may be compromised through SQL injection, social engineering techniques may be applied, or any other technique agreed upon with the client in order to achieve the final objective.

### Post exploitation

In the first phase, we will have determined with the client the level of intrusion to be carried out, and we must ensure that both parties agree on the procedures to be followed. Based on this, during this phase the possible ways in which an attacker could escalate privileges, deny a service, gain access to specific data, and so on, are identified.

### Reporting

Once the technical part of a penetration test has been completed, a series of reports will be delivered to the client presenting the results of the work performed. These reports are often the **only tangible** deliverable the client receives and what they are ultimately paying for.

Moreover, they are frequently the only way to justify the cost incurred, and since this presentation of results represents the only visible face and public image of the security company, it is essential that it reflects the best possible image.

## ISSAF

The ISSAF standard (Information System Security Assessment Framework) provides an even more structured and specialized approach to penetration testing than the PTES methodology. If the unique situation of your organization **requires an advanced methodology fully tailored to its context**, this framework can be especially useful for the specialists responsible for conducting the penetration test.

## NIST SP 800-115

NIST SP 800-115 (Technical Guide to Information Security Testing and Assessment) provides a comprehensive framework for planning, conducting, and reporting security testing activities. Developed by the National Institute of Standards and Technology, this guide is widely used in **government and enterprise environments** and covers techniques such as penetration testing, vulnerability scanning, and security assessments, ensuring a structured and repeatable approach to evaluating an organization’s security posture.