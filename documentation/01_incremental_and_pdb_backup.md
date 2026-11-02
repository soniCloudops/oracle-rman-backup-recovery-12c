\# Scenario 1: Oracle RMAN Incremental and PDB Backups



\## 1. Level 0 Incremental Backup



Script: backup/level0\_backup.rman



Purpose:

\- Creates the baseline incremental backup.

\- Acts as the parent for subsequent Level 1 backups.

\- Suitable for weekly baseline backup schedules.



Command:

BACKUP INCREMENTAL LEVEL 0 DATABASE;



\## 2. Level 1 Differential Backup



Script: backup/level1\_differential\_backup.rman



Purpose:

\- Backs up blocks changed since the most recent Level 0 or Level 1 backup.

\- Generally produces smaller daily backups.

\- Suitable for daily incremental backup schedules.



Command:

BACKUP INCREMENTAL LEVEL 1 DATABASE;



\## 3. Level 1 Cumulative Backup



Script: backup/level1\_cumulative\_backup.rman



Purpose:

\- Backs up blocks changed since the most recent Level 0 backup.

\- Can simplify incremental recovery.

\- Usually larger than differential backups.



Command:

BACKUP INCREMENTAL LEVEL 1 CUMULATIVE DATABASE;



\## 4. PDB Backup



Script: backup/pdb\_backup.rman



Purpose:

\- Backs up a selected Pluggable Database.

\- Useful for independent PDB protection.

\- Avoids backing up the entire CDB when only one PDB is required.



Command:

BACKUP PLUGGABLE DATABASE PDB\_NAME;



\## Verification



Run inside RMAN:



LIST BACKUP SUMMARY;

LIST BACKUP OF DATABASE;

LIST BACKUP TAG 'LEVEL0\_WEEKLY';

LIST BACKUP TAG 'LEVEL1\_DIFFERENTIAL';

LIST BACKUP TAG 'LEVEL1\_CUMULATIVE';

LIST BACKUP TAG 'PDB\_BACKUP';



\## Important Notes



\- Run the PDB backup while connected to the CDB root.

\- Replace PDB\_NAME with the actual PDB name.

\- Ensure backup destinations exist on the database server.

\- Level 1 differential and cumulative backups have different recovery requirements.

\- Test backup and recovery procedures in a lab environment.

