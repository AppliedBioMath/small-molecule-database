# small-molecule-database
This project aims to create locally accessible chemical DBMS.
DBMS contains ChEMBL29, CHEBI and eMolecules
1.Data sources
ChEMBL29 download link https://ftp.ebi.ac.uk/pub/databases/chembl/ChEMBLdb/latest/chembl_29_postgresql.tar.gz (unzip to chembl_29_postgresql.dmp)
CHEBI download link for https://ftp.ebi.ac.uk/pub/databases/chebi/generic_dumps/generic_dump_allstar.zip (unzip to tables.sql) and
https://ftp.ebi.ac.uk/pub/databases/chebi/generic_dumps/pgsql_create_tables.sql (unzip to pgsql_create_tables.sql)
eMolecules https://downloads.emolecules.com/free/2021-12-01/version.sdf.gz (unzip to version.sdf)
2. Import database into postgresql
a.Create the database: Log into PostgreSQL database server where you intend to load chembl data and run the following command to create new database:
```
    psql create database chemicals;
```
Logout of database

b. ChEMBL29 
use command line to load data and replace <username>, <password> with local settings,
'''
psql -u <username> -p <password> chemicals < chembl_29_postgresql.dmp
'''
c. CHEBI
use command line to load creating tables data first and replace <username>, <password> with local settings,
'''
psql -u <username> -p <password> chemicals < pgsql_create_tables.sql
'''
followed by import database
'''
psql -u <username> -p <password> chemicals < tables.sql
'''
d. eMolecules
There is no .dmp or .sql file provided by eMolecules, so that it cannot be imported into DBMS directly. 
version.sdf is the .sdf file which contains the chemicals entity which can be parsed by RDKit (https://www.rdkit.org/docs/GettingStartedInPython.html)
The parsed chemical can be imported into the DBMS via the sqlchemy.
The script is listed as eMolecules_import.ipynb
