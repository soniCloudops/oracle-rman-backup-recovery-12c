\# Scenario 4: Control File and SPFILE Recovery



\## Objective

Recover the Oracle database after losing the SPFILE or control files.



\## Scenario A: SPFILE Loss



1\. Prepare a temporary PFILE.

2\. Start the instance in NOMOUNT mode using the PFILE.

3\. Set the database DBID.

4\. Restore the SPFILE from autobackup.

5\. Restart the instance using the restored SPFILE.



\## Scenario B: Control File Loss



1\. Ensure the SPFILE is available.

2\. Start the instance in NOMOUNT mode.

3\. Set the database DBID.

4\. Restore the control file from autobackup.

5\. Mount the database.

6\. Restore database files if required.

7\. Recover the database.

8\. Open the database with RESETLOGS.



\## Important RMAN Commands



```rman

SET DBID 1234567890;

RESTORE SPFILE FROM AUTOBACKUP;

RESTORE CONTROLFILE FROM AUTOBACKUP;

ALTER DATABASE MOUNT;

RESTORE DATABASE;

RECOVER DATABASE;

