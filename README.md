# small-molecule-database
This project aims to create locally accessible chemical DBMS.  
DBMS contains ChEMBL29, CHEBI and eMolecules  
1.Data sources  
ChEMBL29 download link https://ftp.ebi.ac.uk/pub/databases/chembl/ChEMBLdb/latest/chembl_29_postgresql.tar.gz (unzip to chembl_29_postgresql.dmp)  
CHEBI (version Dec.2021) download link for https://ftp.ebi.ac.uk/pub/databases/chebi/generic_dumps/generic_dump_allstar.zip (unzip to tables.sql) and https://ftp.ebi.ac.uk/pub/databases/chebi/generic_dumps/pgsql_create_tables.sql (unzip to pgsql_create_tables.sql)  
eMolecules (version Dec.2021) https://downloads.emolecules.com/free/2021-12-01/version.sdf.gz (unzip to version.sdf)  
2. Import database into postgresql  
For those who first use the postgresql, check this blog https://phoenixnap.com/kb/install-postgresql-windows.  
a.Create the database: 
Log into PostgreSQL database server in command line where you intend to load data:
```
psql -U <username> -p <password>
```
Create database inside
```
postgres=# create database chemicals;
```
Logout of database with \q  

b. ChEMBL29 
use command line to load data and replace <username>, <password> with local settings,
```
psql -U <username> -p <password> chemicals < chembl_29_postgresql.dmp
```
c. CHEBI
use command line to load creating tables data first and replace <username>, <password> with local settings,
```
psql -U <username> -p <password> chemicals < pgsql_create_tables.sql
```
followed by import database
```
psql -U <username> -p <password> chemicals < tables.sql
```
d. eMolecules
There is no .dmp or .sql file provided by eMolecules, so that it cannot be imported into DBMS directly.   
version.sdf is the .sdf file which contains the chemicals entity which can be parsed by RDKit (https://www.rdkit.org/docs/GettingStartedInPython.html)  
The parsed chemical can be imported into the DBMS via the sqlchemy.  
The script is listed as eMolecules_import.ipynb  
3. Query the concatenated databases
Here is a brief tutorial for query https://www.w3schools.com/sql/sql_join.asp. Inside the DBMS (DBeaver recommanded) join the information among the tables
```
select * from <table a> a
join <table b> b on a.<column> = b.<column>
where <filter condition>;
```
