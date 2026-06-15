# codepath-cybersecurity-project2
A hands-on implementation of system auditing and behavioral analysis using the Linux Audit Daemon (`auditd`). In this project, I configured active kernel-level traps to detect unauthorized file system modifications and tracked down the origins of automated attack scripts.


## Core Concepts Implemented
* **System Auditing**: Installed and managed the Linux audit service daemon.
* **Kernel-Level File Watches**: Configured rule sets targeting directory hierarchies for write/attribute mutations (`-p wa`).
* **Log Parsing & Forensic Analysis**: Leveraged `ausearch` and data filtering utilities (`grep`) to trace system calls back to originating binaries.

## Implementation Steps

### 1. Installation & Environment Setup
First, I ensured the Linux Audit service framework was running on the system:


### 2. Configuring File Integrity Watches
I established a directory-wide watch rule with a persistent tracking key (`files_changes`) to monitor the target `/protected_files` workspace:

*To make these rules permanent across reboots, I appended them to `/etc/audit/rules.d/audit.rules` using the `vi` editor.*

### 3. Attack Execution & Log Interception
After granting executable permissions, three attack scripts (`attack-a`, `attack-b`, `attack-c`) were fired against the directory structure. 

I then parsed the raw audit entries using `ausearch` to pair the attacker's binary (`exe`) with the targeted document (`name`):

## Forensic Findings
By mapping corresponding timestamps and system event IDs, I verified the following layout:
* **Affected Files**: cloudia.txt, oakley.txt, squeaky.txt, precipitation.csv 

* **Attacker Pairings**:
  * `(cloudia.txt, attack-a)`
  * `(oakley.txt, attack-b)`
  * `(squeaky.txt, attack-b)`
  * `(precipitation.csv, attack-c)`
