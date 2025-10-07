Student Name: MUREKEZI SANGWA Fabrice

Student ID: 28395

Course: PL/SQL and Database Administration
________________________________________
1. Introduction
The aim of the task was focusing on how to work with Oracle 21c Multitenant Architecture, particularly the creation, management, and deletion of Pluggable Databases (PDBs) within a Container Database (CDB).
The main objectives were:
•	      To understand and apply commands such as CREATE, ALTER and DROP PLUGGABLE DATABASE.
•	To create a new pluggable database for classwork.
•	To create and delete another pluggable database for practice.
•	To verify the operations using Oracle Enterprise Manager (OEM).
________________________________________
2. Environment Setup
•	Operating System: Windows 10 Pro
•	Tools Used:
o	SQL*Plus
o	SQL Developer
o	Oracle Enterprise Manager (OEM)
NOTE: Before starting, the Oracle listener and database services were verified to be running using: services.msc
________________________________________
3. Task 1 – Creating the First Pluggable Database


Explanation:
•	CREATE PLUGGABLE DATABASE – creates a new PDB within the container.
•	ADMIN USER – defines the administrator for this PDB.
•	CREATE_FILE_DEST – specifies where Oracle will store the new database files.
•	ALTER PLUGGABLE DATABASE ... OPEN READ WRITE – opens the PDB for use.
•	SAVE STATE – ensures it reopens automatically on database restart.
Result:
The PDB was created successfully and appeared under SHOW PDBS as READ WRITE.
 
<img width="975" height="205" alt="image" src="https://github.com/user-attachments/assets/bf288072-22dc-4aa8-b991-27bb7fbc8708" />

<img width="940" height="338" alt="image" src="https://github.com/user-attachments/assets/26ce6655-a4cb-4df9-88e2-ac33dc70387a" />

 


________________________________________
4. Task 2 – Creating and Deleting a Second PDB
Objective:
Create another pluggable database named fa_to_delete_pdb_28395 and then delete it to demonstrate full database lifecycle management.
ALTER PLUGGABLE DATABASE fa_to_delete_pdb_28395 OPEN READ WRITE;
SHOW PDBS;
This screenshot showing fa_to_delete_pdb_28395 in READ WRITE mode.  
<img width="975" height="184" alt="image" src="https://github.com/user-attachments/assets/13a37898-9677-4da1-8942-4d6c63f043c5" />
________________________________________
Deletion Procedure
SQL Script (Deletion):
ALTER PLUGGABLE DATABASE fa_to_delete_pdb_28395 CLOSE IMMEDIATE;
DROP PLUGGABLE DATABASE fa_to_delete_pdb_28395 INCLUDING DATAFILES;
SHOW PDBS;
Explanation:
•	The PDB must be closed before deletion.
•	INCLUDING DATAFILES ensures that all associated files are removed from disk.
•	SHOW PDBS confirms removal from the container database.
Output after executing DROP command showing the PDB is no longer listed  

<img width="940" height="338" alt="image" src="https://github.com/user-attachments/assets/1af0713d-7842-4114-a833-a976c823568b" />

<img width="854" height="257" alt="image" src="https://github.com/user-attachments/assets/ba20ac98-aadb-485b-a1b9-17d9562a2973" />
________________________________________
5. Task 3 – Managing PDBs via Oracle Enterprise Manager (OEM)
Objective:
Verify the existence and status of PDBs using the graphical interface of Oracle Enterprise Manager.
Procedure:
1.	Accessed OEM at:
2.	https://localhost:5500/em
3.	Logged in using the SYS user in Container Database (CDB) mode.
4.	Navigated to:
Container Database → Pluggable Databases
	Verified: FA_PDB28395 appears as OPEN (READ WRITE).
o	fa_to_delete_pdb_28395 no longer exists after deletion.
o	OEM interface showing the active PDBs list.

<img width="940" height="467" alt="image" src="https://github.com/user-attachments/assets/eb40e73c-8ad7-4ab4-a359-488c2c4af352" />
   

________________________________________
6. Error Handling and Troubleshooting
So some common errors that was faced during the extraction of our task and the methods that was used to handle them.  
Error Code	Description	Solution Applied
ORA-65005	Invalid or missing file path in FILE_NAME_CONVERT	Replaced with CREATE_FILE_DEST for simplicity.
ORA-65011	PDB does not exist	Verified creation success before attempting ALTER.
ORA-00933	SQL command not properly ended	Executed one statement at a time; avoided chaining with semicolons.
ORA-12541	Listener not running	Started Oracle Listener service via services.msc.
ORA-65019	PDB already open	Checked current PDB state with SHOW PDBS before running ALTER.
________________________________________
7. Understanding PDB States
State	Description	Purpose
MOUNTED	The PDB is recognized by Oracle but not yet opened.	Used during startup or maintenance.
READ ONLY	The PDB is open for reading data only.	Used for reports or seed databases (like PDB$SEED).
READ WRITE	The PDB is fully open and editable.	Allows all SQL operations (SELECT, INSERT, UPDATE, DELETE).
Example Commands:
ALTER PLUGGABLE DATABASE FA_PDB28395 OPEN READ WRITE;
________________________________________
8. Role of the ALTER Command
ALTER is used to modify the state or structure of existing database objects.
•	In this assignment, it was used to open, close, and save the state of PDBs:
•	ALTER PLUGGABLE DATABASE pdb_fa28395 OPEN READ WRITE;
•	ALTER PLUGGABLE DATABASE pdb_fa28395 SAVE STATE;
•	ALTER PLUGGABLE DATABASE fa_to_delete_pdb_28395CLOSE IMMEDIATE;
•	It changes behaviour, not structure — unlike CREATE (to make new) or DROP (to remove).
________________________________________
9. Conclusion
This exercise provided hands-on experience with Oracle Multitenant Architecture, demonstrating:
•	The process of creating, opening, saving, and deleting PDBs.
•	The use of ALTER for managing database states.
•	Troubleshooting common Oracle errors effectively.
•	Confirming results using Oracle Enterprise Manager (OEM).
Through this practical, I gained confidence in using Oracle SQL commands and better understanding the relationship between the CDB (Container Database) and PDBs (Pluggable Databases).
________________________________________
so here is the source for the used data
 References
1.	Oracle® Database 21c: Multitenant Administrator’s Guide
Oracle Corporation, 2023.
Available at: https://docs.oracle.com/en/database/oracle/oracle-database/21/multi/index.html
2.	Oracle Learning Library (OLL) – Tutorials on Oracle Multitenant Architecture.
https://apexapps.oracle.com/pls/apex/f?p=44785:141:0
3.	Oracle LiveSQL – Interactive SQL practice environment.
https://livesql.oracle.com
________________________________________
Citation Format:
Use APA or IEEE referencing depending on your instructor’s preference. The above list follows a simple academic format suitable for GitHub or report documentation.

________________________________________

