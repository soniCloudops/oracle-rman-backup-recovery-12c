# Oracle RMAN Backup & Recovery – Oracle Database 12c

A practical Oracle DBA project demonstrating RMAN backup strategies, incremental backups, archive log management, Pluggable Database (PDB) backups, database restoration, and disaster recovery.

This repository contains reusable RMAN scripts and documentation for learning and practising Oracle Database 12c backup and recovery operations.

## Project Objectives

- Understand Oracle RMAN backup types and strategies.
- Implement Level 0 and Level 1 incremental backups.
- Compare differential and cumulative incremental backups.
- Perform archive log backups.
- Back up individual Pluggable Databases.
- Practise complete database restore and recovery.
- Understand SPFILE and control file recovery.
- Perform point-in-time recovery (PITR).

## Technologies

- Oracle Database 12c
- Recovery Manager (RMAN)
- Linux / Unix
- SQL and PL/SQL
- Oracle backup and recovery architecture

## Repository Structure

```text
oracle-rman-backup-recovery-12c/
│
├── backup/
│   ├── archive_log_backup.rman
│   ├── level0_backup.rman
│   ├── level1_differential_backup.rman
│   ├── level1_cumulative_backup.rman
│   ├── pdb_backup.rman
│   └── controlfile_spfile_backup.rman  (placeholder)
│
├── recovery/
│   ├── complete_restore_recover.rman
│   ├── spfile_recovery.rman
│   ├── controlfile_recovery.rman
│   ├── point_in_time_recovery.rman
│   ├── restore_recover_database.rman   (placeholder)
│   └── validate_backup.rman            (placeholder)
│
├── documentation/
│   ├── 01_incremental_and_pdb_backup.md
│   ├── 04_controlfile_spfile_recovery.md
│   └── 05_point_in_time_recovery.md
│
└── README.md
```

Files marked as placeholders are currently empty and are not completed procedures.

## Backup Scenarios

### Scenario 1: Incremental Database Backup

| Script | Purpose |
|---|---|
| [level0_backup.rman](backup/level0_backup.rman) | Creates the baseline Level 0 incremental backup. |
| [level1_differential_backup.rman](backup/level1_differential_backup.rman) | Backs up changes since the most recent Level 0 or Level 1 backup. |
| [level1_cumulative_backup.rman](backup/level1_cumulative_backup.rman) | Backs up changes since the most recent Level 0 backup. |
| [pdb_backup.rman](backup/pdb_backup.rman) | Backs up a selected Pluggable Database. |

**Why use incremental backups?**

Incremental backups reduce the amount of data that needs to be backed up compared with repeatedly taking full database backups.

- Level 0: Baseline for the incremental backup strategy.
- Level 1 Differential: Generally smaller daily backups.
- Level 1 Cumulative: Can simplify recovery by reducing the number of incremental backup sets required.
- PDB Backup: Protects an individual Pluggable Database.

Detailed documentation: [Scenario 1 – Incremental and PDB Backup](documentation/01_incremental_and_pdb_backup.md)

### Scenario 2: Archive Log Backup

Script: [archive_log_backup.rman](backup/archive_log_backup.rman)

**Topics covered:**
- Archive log backup using RMAN.
- Compressed backup sets.
- `NOT BACKED UP 1 TIMES` clause.
- Backup channel allocation.
- Archive log backup management.

**Why is archive log backup important?**

Archive logs contain the redo information required for database recovery. Regular archive log backups help support recovery to a desired point in time.

### Scenario 3: Complete Database Restore and Recovery

Script: [complete_restore_recover.rman](recovery/complete_restore_recover.rman)

**Topics covered:**
- Checking available RMAN backups.
- Shutting down the database.
- Starting the database in MOUNT mode.
- Restoring database files.
- Applying archived redo using recovery.
- Opening the database after complete recovery.

**Why is it important?**

This procedure demonstrates how to restore database files and recover the database using available backups and redo.

### Scenario 4: SPFILE and Control File Recovery

Scripts:

- [spfile_recovery.rman](recovery/spfile_recovery.rman)
- [controlfile_recovery.rman](recovery/controlfile_recovery.rman)

**Topics covered:**
- Database DBID.
- SPFILE restoration from autobackup.
- Control file restoration from autobackup.
- NOMOUNT and MOUNT startup modes.
- Database restore and recovery.
- Opening with RESETLOGS when recovering using a backup control file.

Documentation: [Control File and SPFILE Recovery](documentation/04_controlfile_spfile_recovery.md)

**Why is it important?**

The SPFILE contains database initialization parameters, while the control file maintains important database structure and backup metadata. Losing either can prevent normal database startup or recovery.

### Scenario 5: Point-in-Time Recovery (PITR)

Script: [point_in_time_recovery.rman](recovery/point_in_time_recovery.rman)

**Topics covered:**
- Incomplete database recovery.
- Recovery using a target timestamp.
- RESTORE and RECOVER operations.
- Opening the database with RESETLOGS.

Documentation: [Point-in-Time Recovery](documentation/05_point_in_time_recovery.md)

**Why is it important?**

PITR helps recover a database to a point before an unwanted transaction, logical error, or data corruption occurred. Transactions after the selected recovery point are not retained in the recovered database.

## How to Execute RMAN Scripts

### 1. Clone the repository

```bash
git clone https://github.com/soniCloudops/oracle-rman-backup-recovery-12c.git
```

### 2. Navigate to the repository

```bash
cd oracle-rman-backup-recovery-12c
```

### 3. Connect to RMAN

For a local database connection:

```bash
rman target /
```

### 4. Execute a backup script

Example – Level 0:

```rman
@backup/level0_backup.rman
```

Example – Level 1 Differential:

```rman
@backup/level1_differential_backup.rman
```

Example – Archive Log Backup:

```rman
@backup/archive_log_backup.rman
```

Example – PDB Backup:

```rman
@backup/pdb_backup.rman
```

### 5. Execute a recovery script

Example:

```rman
@recovery/complete_restore_recover.rman
```

Recovery scripts contain operations that can overwrite or change database files and database state. Review all prerequisites before execution.

## Important DBA Considerations

- Ensure the database is configured in ARCHIVELOG mode where required.
- Verify backup destination paths and available storage.
- The current scripts use `/backup/rman/`, which assumes a Linux database server and an existing writable directory.
- Replace `PDB_NAME` with the actual PDB name.
- Replace sample DBID values and recovery timestamps with environment-specific values.
- Review RMAN retention and archive log deletion policies.
- Validate backups and periodically test restore and recovery.
- Take a fresh backup after an incomplete recovery and `OPEN RESETLOGS`.
- Never run recovery scripts against production without an approved recovery plan.

**Note:** These scripts are practical learning templates. Validate syntax, database version compatibility, configuration, and recovery prerequisites in a lab before production use.

## Author

**Soni Sharma**

Oracle DBA | Linux System Engineer

## GitHub Repository

[Oracle RMAN Backup & Recovery – Oracle 12c](https://github.com/soniCloudops/oracle-rman-backup-recovery-12c)