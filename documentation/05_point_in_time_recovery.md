\# Scenario 5: Oracle RMAN Point-in-Time Recovery (PITR)



\## Objective

Recover an Oracle database to a specific point in time.



\## Use Cases

\- Accidental table or data deletion

\- Incorrect application deployment

\- Logical data corruption

\- User error or unwanted transactions



\## Recovery Procedure



1\. Identify the required recovery timestamp.

2\. Verify database backups.

3\. Verify archive log availability.

4\. Shut down the database.

5\. Start the database in MOUNT mode.

6\. Set the recovery timestamp.

7\. Restore the database.

8\. Recover the database.

9\. Open using RESETLOGS.



\## RMAN Commands



```rman

SHUTDOWN IMMEDIATE;

STARTUP MOUNT;



RUN {

&#x20;   SET UNTIL TIME

&#x20;       "TO\_DATE('2026-11-02 14:30:00',

&#x20;                'YYYY-MM-DD HH24:MI:SS')";



&#x20;   RESTORE DATABASE;

&#x20;   RECOVER DATABASE;

}



SQL 'ALTER DATABASE OPEN RESETLOGS';

