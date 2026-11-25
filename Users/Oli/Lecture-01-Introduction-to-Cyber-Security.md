# Lecture 01 – Introduction to Cyber Security

**Course:** T-401-ICYB – Introduction to Cyber Security  
**Lecture date:** 23 November 2026  
**Lecturer:** Stephan Schiffel

---

## 1. Introduction to Cyber Security

Cyber security is the practice of protecting computers, networks, applications, systems and data from unauthorized access, attacks, damage or disruption.

The main goals are to protect information and ensure that systems continue to operate safely and reliably.

Cyber security includes:
- Preventing attacks.
- Detecting suspicious activity.
- Responding to security incidents.
- Recovering systems after an attack.
- Reducing security risks before they become problems.

### Why is Cyber Security Important?

Modern organizations depend on digital systems to store information, communicate and provide services.

A security incident can cause:
- Financial losses.
- Loss of sensitive information.
- Damage to an organization's reputation.
- Disruption of services.
- Legal and regulatory consequences.

Cyber security is therefore important for individuals, companies, governments and society.

## 2. Attack Surface

An **attack surface** is the collection of all possible points where an attacker could try to enter or interact with a system.

Examples include:
- Open network ports.
- Websites and web applications.
- User accounts and login pages.
- Email attachments.
- Software vulnerabilities.
- Remote access services.
- USB devices and other external connections.

### Reducing the Attack Surface

The fewer unnecessary entry points a system has, the fewer opportunities an attacker has to exploit it.

Ways to reduce the attack surface:
1. Disable unnecessary services.
2. Close unused network ports.
3. Remove unused software.
4. Apply security updates.
5. Use strong authentication.
6. Restrict user permissions.
7. Configure firewalls correctly.

**Example:** If a computer runs a network service that is not needed, disabling that service removes a potential entry point for attackers.

## 3. The History and Development of Cyber Attacks

Cyber attacks have changed as computers and networks have developed.

Early attacks often involved experimentation, viruses and worms. Modern attacks are frequently more organized and may be financially or politically motivated.

Common developments include:
- Early computer viruses spreading through infected files.
- Network worms spreading automatically between computers.
- Trojan software pretending to be legitimate programs.
- Ransomware encrypting files and demanding payment.
- Attacks targeting businesses, governments and critical infrastructure.

### Important Lesson

Cyber security is constantly changing. New technologies create new opportunities for attackers, so security methods must also evolve.

## 4. Malware

**Malware** means malicious software. It is software designed to harm a computer, steal information, gain unauthorized access or perform other unwanted actions.

### Common Types of Malware

| Type | Explanation |
|---|---|
| Virus | Attaches itself to another file or program and spreads when that file is executed. |
| Worm | Self-replicates and spreads between systems, often over networks. |
| Trojan horse | Pretends to be legitimate software but performs malicious actions. |
| Ransomware | Locks or encrypts data and demands payment. |
| Spyware | Secretly collects information about a user or system. |
| Rootkit | Hides malicious activity and helps an attacker maintain privileged access. |

### Virus vs. Worm vs. Trojan

These terms are related but describe different behaviours.

- **Virus:** Usually needs a host file or program to spread.
- **Worm:** Can spread independently between systems.
- **Trojan:** Tricks users into installing or running malicious software by pretending to be legitimate.

**Example:** A user downloads a fake application. The application appears normal but secretly installs malware. This is an example of a Trojan horse.

## 5. Malware Mechanisms

Malware may use several techniques to remain active and communicate with attackers.

### Persistence

Persistence means that malware attempts to remain active after a system restarts or after a user logs out.

Examples include:
- Adding programs to startup locations.
- Creating scheduled tasks.
- Modifying system configuration.
- Installing malicious services.

### Command and Control (C2)

Command and Control refers to communication between an infected system and an attacker's infrastructure.

A C2 server may allow an attacker to:
- Send commands to infected computers.
- Receive stolen information.
- Monitor compromised systems.
- Coordinate multiple infected devices.

### Typical Malware Process

1. **Delivery:** Malware reaches the target through an attachment, download or vulnerability.
2. **Execution:** The malicious code runs.
3. **Persistence:** The malware attempts to remain on the system.
4. **Communication:** It may contact a Command and Control server.
5. **Action:** It steals information, encrypts files or performs another malicious activity.

## 6. The CIA Triad

The CIA triad is one of the most important models in information security.

It consists of three principles:

### Confidentiality

Information should only be accessible to authorized people or systems.

Examples:
- Password protection.
- Encryption.
- Access permissions.
- Multi-factor authentication.

**Security failure:** An attacker accesses private customer information.

### Integrity

Information should remain accurate, complete and protected from unauthorized modification.

### Common Types of Malware

| Type | Explanation |
|---|---|
| Virus | Attaches itself to another file or program and spreads when that file is executed. |
| Worm | Self-replicates and spreads between systems, often over networks. |
| Trojan horse | Pretends to be legitimate software but performs malicious actions. |
| Ransomware | Locks or encrypts data and demands payment. |
| Spyware | Secretly collects information about a user or system. |
| Rootkit | Hides malicious activity and helps an attacker maintain privileged access. |
