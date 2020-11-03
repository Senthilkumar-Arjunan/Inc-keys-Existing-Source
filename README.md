# Inc-keys-Existing-Source

# Requirement
Merge two source files and increment the id column
# Source File 1
id,name,gender,department

1,senthil,male,ECE

2,kumar,male,CSC

3,vaishnavi,female,ECE

# Source File 2

name,gender,department

Kuna,female,EEE

prasath,male,CSC

meena,female,EEE

# Expected output

id,name,gender,department

1,senthil,male,ECE

2,kumar,male,CSC

3,vaishnavi,female,ECE

4,Kuna,female,EEE

5,prasath,male,CSC

6,meena,female,EEE

# Services used

Azure Blob Storage

Azure ADF

# Steps Followed

1. Import the both file into Blop storage

2. Created New DataFlow in ADF

3. Created the source dataset for source file 1 (Including ID column)

4. Added dummy column using "Derived Column" schema (We need to apply aggregate function, all columns are unique field. So we added one dummy column)

5. Apply Aggregate function. Group By based on dummy column and aggregate max(id) => assigned into max id column

6. Added Source2 (Without id column) and Join with above step 5 (Cross join codition 1==1)

7. Added Suragate Key (Which is used to increment the column based on start value)

8. Added again Derived Column with this condition id = maxid + suragte key id 

9. choose Select operation to remove unwanted columns (dummy and maxid)

10. Create brach from source file 1

11. union source file 1 and select output (step 9 )

12. Created Sink (Target Blop)

13. Create new pipeline and Publish & Trigger it
