# Bicycle Rental and Selling Shop Database Project

## Project Overview
This project focuses on creating a **Bicycle Rental and Selling Shop** database system using Oracle SQL and PL/SQL. The system supports basic operations such as managing bicycles, customers, sales, rentals, accessories, and payments.

---

## Features

1. **Database Tables**  
   - `Bicycle`  
   - `Customer`  
   - `Rent`  
   - `Sale`  
   - `Accessories`  
   - `Payment`

2. **Data Manipulation**  
   - Insert, update, and delete operations for all tables.  

3. **Queries**  
   - Nested subqueries  
   - Joins (INNER, LEFT, RIGHT, FULL OUTER)  
   - Aggregate functions (`SUM`, `AVG`, `COUNT`, etc.)  
   - Grouping and filtering using `GROUP BY` and `HAVING`.  

4. **Views**  
   - Predefined views for frequently accessed data.  

5. **PL/SQL Programming**  
   - Variable declaration and output.  
   - Cursors for row-by-row processing.  
   - Conditional statements (`IF/ELSE`).  
   - Procedures and Functions to automate data retrieval.  

6. **File Spooling**  
   - Save query results into text files for reporting.

---

## Prerequisites
- **Oracle Database** (e.g., Oracle 11g, 12c, or later).  
- **SQL*Plus or Oracle SQL Developer** for executing scripts.  

---

## How to Run the Project

### Step 1: Database Setup
1. Open your Oracle SQL environment.  
2. Ensure the user is logged in and has necessary permissions.  
   ```sql
   CHECK USER;
   ```
3. Run the script to create tables:  
   ```sql
   CREATE TABLE Bicycle (...);
    CREATE TABLE Customer (...);
    CREATE TABLE Rent (...);
    CREATE TABLE Sale (...);
    CREATE TABLE Accessories (...);
    CREATE TABLE Payment (...);
   ```

### Step 2: Alter and Modify Tables
Run any necessary table modifications or updates:
   ```sql
ALTER TABLE Bicycle ADD rent_H NUMBER(10);
ALTER TABLE Accessories RENAME COLUMN price_A TO price_Acc;
   ```

### Step 3: Insert Sample Data
Execute the provided INSERT statements to populate tables with sample data. Example:
   ```sql
INSERT INTO Bicycle (B_Id, B_Name, model, model_year, price_B, rent_H) 
VALUES ('B001', 'Mountain Bike', 'MTB-1', 2021, 500, 10);
   ```
### Step 4: Execute Queries
Run the predefined queries to view data:
   ```sql
SELECT * FROM Bicycle;  
SELECT AVG(R_Hour) AS average_duration FROM Rent;
   ```

### Step 5: Step 5: PL/SQL Programming
1. Run procedures and functions to automate data processing. Example:
       ```sql
   
            CREATE OR REPLACE PROCEDURE GetCustomerDetails IS
            BEGIN
              FOR cust IN (SELECT * FROM Customer) 
              LOOP
                DBMS_OUTPUT.PUT_LINE('User ID: ' || cust.U_Id || ', Name: ' || cust.U_Name);
              END LOOP;
            END;
            /
            EXECUTE GetCustomerDetails;

       ```

2. Test cursor functionality and IF/ELSE blocks.


## Files Included
  - bicycle_project.sql: Complete database schema, sample data, and queries.
  - plsql_blocks.sql: PL/SQL scripts for variables, procedures, functions, and cursors.

## Key Queries and Results
  1. Display All Data
     ```sql
      SELECT * FROM Bicycle;  
      SELECT AVG(R_Hour) AS average_duration FROM Rent;
     ```
   2. Calculate Total Accessory Revenue
      ```sql
      
                            SELECT B_Id, B_Name, 
                      (SELECT SUM(price_Acc) 
                       FROM Accessories 
                       WHERE B_Id = Bicycle.B_Id) AS total_accessory_revenue
                    FROM Bicycle;
        
       ```   

   3. Identify Bicycles Rented by Older Customers

       ```sql
          SELECT B_Id, B_Name, model 
          FROM Bicycle 
          WHERE B_Id IN (
            SELECT B_Id 
            FROM Rent 
            WHERE U_Id IN (
              SELECT U_Id FROM Customer WHERE age > 25
            )
          );
      
         ```


 ## PL/SQL Demonstration
  1. Function: Fetch Rent Information
     ```sql
                    CREATE OR REPLACE FUNCTION getRentInfo(p_RentId IN Rent.R_Id%TYPE) 
                    RETURN Rent%ROWTYPE IS
                      v_RentInfo Rent%ROWTYPE;
                    BEGIN
                      SELECT * INTO v_RentInfo FROM Rent WHERE R_Id = p_RentId;
                      RETURN v_RentInfo;
                    END;
                    / 
      ```
   2. Procedure: Display Customer Details
      ```sql
                  CREATE OR REPLACE PROCEDURE GetCustomerDetails IS
                  BEGIN
                    FOR cust IN (SELECT * FROM Customer) 
                    LOOP
                      DBMS_OUTPUT.PUT_LINE('User ID: ' || cust.U_Id || ', Name: ' || cust.U_Name);
                    END LOOP;
                  END;
                  /
       ```

  ## Output Files  
  To save query outputs to files, use the SPOOL command:
   ```sql
                      SPOOL "D:\Database LAB\OUTPUT\Bicycle.txt"
                      SELECT * FROM Bicycle;
                      SPOOL OFF;
   ```
  ## Notes  
- Ensure the database server is running before executing scripts.  
- Modify file paths for `SPOOL` commands to match your local directory structure.  
- Review all queries before execution to match specific project requirements.
  
## License

This project is licensed under the MIT License - see the LICENSE file for details

## Contact

For any queries or contributions, please contact:

**Developer:** Aciful Islam Khan   
**Email:** sopnil493@gmail.com 
**GitHub:**  https://github.com/Elin-powS               
