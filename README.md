# oracle-rman-backup-recovery-12c



A practical Oracle DBA project demonstrating RMAN backup strategies, database restoration, disaster recovery, and point-in-time recovery procedures.



\## Project Overview



This repository contains practical Oracle Recovery Manager (RMAN) scripts and documentation for Oracle Database 12c.



The objective is to demonstrate hands-on knowledge of Oracle database backup and recovery, backup automation, archive log management, and disaster recovery scenarios.



\## Technologies Used



\- Oracle Database 12c

\- Oracle Recovery Manager (RMAN)

\- Linux / Unix

\- SQL and PL/SQL

\- Shell Scripting



\## Scenarios Covered



\### Scenario 1: Incremental Database Backup



\- Level 0 incremental backup

\- Level 1 differential incremental backup

\- Level 1 cumulative incremental backup

\- Backup strategy and scheduling



\### Scenario 2: Archive Log Backup



\- Archive log backup using RMAN

\- Compressed backup sets

\- `NOT BACKED UP` optimization

\- Archive log deletion considerations



\### Scenario 3: Complete Database Restore and Recovery



\- Database shutdown and mount

\- Database restore

\- Database recovery

\- Database opening after complete recovery



\### Scenario 4: Control File and SPFILE Recovery



\- SPFILE restoration from autobackup

\- Control file restoration

\- NOMOUNT and MOUNT startup modes

\- Database recovery using a backup control file



\### Scenario 5: Point-in-Time Recovery (PITR)



\- Incomplete database recovery

\- Recovery using a timestamp

\- Recovery using an SCN

\- Opening the database with RESETLOGS



\## Repository Structure



```text

oracle-rman-backup-recovery-12c/

│

├── backup/

│   ├── level0\_backup.rman

│   ├── level1\_differential\_backup.rman

│   ├── level1\_cumulative\_backup.rman

│   ├── archive\_log\_backup.rman

│   ├── controlfile\_spfile\_backup.rman

│   └── pdb\_backup.rman

│

├── recovery/

│   ├── complete\_restore\_recover.rman

│   ├── spfile\_recovery.rman

│   ├── controlfile\_recovery.rman

│   └── point\_in\_time\_recovery.rman

│

├── documentation/

│   ├── 02\_archive\_log\_backup.md

│   ├── 04\_controlfile\_spfile\_recovery.md

│   └── 05\_point\_in\_time\_recovery.md

│

├── linux-scripts/

│

└── README.md

```



\## Prerequisites



\- Oracle Database 12c environment

\- RMAN access to the target database

\- Database configured in ARCHIVELOG mode for online archive log backup and recovery

\- Configured backup destination with sufficient storage

\- Required database backups and archive logs available



\## How to Use



\### 1. Clone the repository



```bash

git clone https://github.com/soniCloudops/oracle-rman-backup-recovery-12c.git

```



\### 2. Connect to RMAN



```bash

rman target /

```



\### 3. Execute an RMAN script



For example:



```rman

@backup/level0\_backup.rman

```



Or execute a recovery script:



```rman

@recovery/point\_in\_time\_recovery.rman

```



Review each script and update database-specific parameters, backup locations, and recovery targets before execution.



\## Important DBA Notes



\- Validate backup availability before starting recovery.

\- Monitor archive log generation and backup completion.

\- Keep control file and SPFILE autobackups enabled.

\- Verify backup retention and deletion policies.

\- PITR is an incomplete recovery operation; transactions after the recovery point are not included.

\- Take a new backup after opening the database with RESETLOGS.

\- Test all recovery procedures in a controlled lab environment.



\*\*Warning:\*\* These scripts are learning examples. Never execute destructive restore or recovery operations on production databases without an approved recovery plan.



\## Author



\*\*Soni Sharma\*\*



Oracle DBA | Linux System Engineer



\## GitHub Repository



\[Oracle RMAN Backup \& Recovery – Oracle 12c](https://github.com/soniCloudops/oracle-rman-backup-recovery-12c)

