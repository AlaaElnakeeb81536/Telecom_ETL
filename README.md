# Telecom_ETL
 ETL Case Study Project for Telecom Company using SQL Server Integration Services (SSIS)
# Project Description
 Telecom-ETL is an ETL Package that extracts and ingests event data from multiple telecomunication industry files and stores the data in a relational database.

-A telecommunications company has approached you as an ETL developer/consultant to undertake a data warehousing process as follows
The company has a system that generally saves a periodic csv file every 5 pm, and this file includes basic data for the various movements made by customers during a specific period of time.
I provided you with the following table, which shows the data stored in the csv file
 ![image](https://github.com/user-attachments/assets/17a1763a-4aca-4616-be2c-582a9ba13909)

 # The processing required to be completed on this data before it is stored in the database
![image](https://github.com/user-attachments/assets/3effae61-14c2-4709-930d-a9cb589fbb9a)

-Rejected transactions will be stored in a separate table, with the original csv file name recorded

-During the process of recording data in the database, there are some additional data that are required to be recorded to ensure the quality of the data storage process
1-Number of animations in the csv file
2-The number of transactions stored in the database
3-The number of transactions rejected because the required conditions were not met
4-Link data stored in the database with the original csv file

After completing the process of storing data in the database according to the previous conditions, move the csv file to another folder

# Tools
SQL Server - SSIS (SQL Server Integration Services)

# Package Design
It consist of Control Flow and Data Flow
# Control Flow
![image](https://github.com/user-attachments/assets/1827dcaf-8dda-465a-bf19-ce175becf558)
### Steps for Data Package Execution and Auditing

1. **Batch ID Generation**: 
   - For each run of the package, generate a new `batch_id` based on the last `batch_id` in the `audit_dim`.
2. **Data Extraction**:
   - Iterate through the data files to extract the necessary data.
3. **Audit Record Insertion**:
   - Insert a new record into the audit dimension, which includes the `batch_id`, package name, and file name.
4. **Data Flow Execution**:
   - Execute the data flow task to load the file data into the database.
   - Capture required auditing data, such as `rejected_rows`, `inserted_rows`, and `all_rows_processed`.
5. **Audit Record Update**:
   - Update the audit record with the number of processed rows, rejected rows, and inserted rows.
6. **File Management**:
   - Move the processed files to a different location for further management.
# Data flow

![image](https://github.com/user-attachments/assets/2c02a36b-1562-4ffc-813b-bfedf0d320a3)

### Data Quality and Auditing Steps

1. **Data Quality Check**:
   - Read data from the files and validate it against predefined data quality rules.
2. **Handling Rejected Data**:
   - If data is rejected from the source, store it in the `error_source_output` table.
3. **Destination Constraints Validation**:
   - If data matches the destination constraints, insert it into the destination table.
   - If data does not match the destination constraints, record it in the `error_destination_output` table.
4. **Auditing Data**:
   - Retrieve the number of rejected and inserted records for auditing purposes.
   - Map the `audit_id` to the corresponding records in the audit tables.
5. **Derived Columns Creation**:
   - Create necessary derived columns, such as `tac` and `snr`, from the `imei` column.
  
   ### Database Schema Design
![image](https://github.com/user-attachments/assets/78f683cc-1cdd-4f6e-babc-9199e2384843)




