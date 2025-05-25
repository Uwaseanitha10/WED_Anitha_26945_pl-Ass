### NAMES :UWASE Anitha
### ID: 26945


### : Hawk Prediction Analytics in a Complex Environment


###  Problem Statement and Project Overview
### 🔍 Problem Definition
Frequent natural disasters disrupt hawk migration and habitat safety.

Lack of real-time analytics for conservation efforts during disasters.

Manual tracking leads to data loss and delayed response.

### 🌍 Context of Use
Wildlife research centers and disaster management agencies.

Real-time monitoring needed during natural events (e.g., storms, wildfires).

Integrated into conservation systems and public safety alerts.

### 🎯 Target Users
Wildlife researchers and ecologists

Disaster response teams

Conservation organizations

Government agencies

### 🎯 Project Goals
Forecast hawk movement during disasters using weather data.

Automate migration alerts and danger zone mapping.

Enhance accuracy and speed of conservation decisions.

Secure and organize tracking data in a PL/SQL database.

### 🎯 Project Objectives

Design a PL/SQL-based Oracle database with multi-entity support.

Integrate predictive algorithms to forecast hawk behavior.

Build disaster-aware habitat monitoring.

### 🗃️ Main Entities
Hawk – ID, species, tag info, age

Disaster – Type, severity, location, duration

Location – GPS, terrain, region risk level

Prediction – Timestamp, movement direction, confidence

Weather – Temp, wind, pressure, conditions

### ✅ Anticipated Benefits
🚀 Real-time hawk movement forecasting

🔒 Secure storage of ecological and disaster data

⚙️ Automated workflows for emergency alerts

📈 Improved conservation strategy and accuracy


### PHASE II
### Business Process Modeling (Related to Management Information Systems - MIS) 
 
### ✅ Defined Scope

### Disaster-Aware Hawk Movement Prediction & Alert System

 


### Scope:
This business process models the interaction between wildlife tracking systems, weather data sources, and disaster management authorities.
The system uses MIS to collect data, run predictive analytics, and disseminate alerts based on hawk movement during natural disasters.

### Objectives:

Automate hawk tracking during disasters.

Enable data-driven decision-making for wildlife protection.

Support real-time alerts to conservation and disaster response teams.

### Expected Outcomes:

Minimized manual data collection.

Accurate and timely predictions.

Enhanced interdepartmental coordination.
Scope:
This business process models the interaction between wildlife tracking systems, weather data sources, and disaster management authorities. The system uses MIS to collect data, run predictive analytics, and disseminate alerts based on hawk movement during natural disasters.

### Objectives:

Automate hawk tracking during disasters.

Enable data-driven decision-making for wildlife protection.

Support real-time alerts to conservation and disaster response teams.

### Expected Outcomes:

Minimized manual data collection.

Accurate and timely predictions.

Enhanced interdepartmental coordination.
### ✅ 2. Key Entities and Roles
  ### Entity	Role / Responsibility
Wildlife Sensor System            	Collects hawk GPS data in real time.
Weather API System	                Supplies live weather data (wind, temp, pressure).
Database (Oracle PL/SQL)          	Stores historical and live hawk movement, weather, and disaster records.
Prediction Engine	                 Uses data to predict hawk flight patterns in disasters.
Wildlife Officer                 	 Verifies predictions and issues alerts if necessary.
Disaster Response Unit	            Uses alerts for evacuation/rescue planning.
MIS Dashboard                     	Visualizes data for decision-makers and generates automated reports.

### ✅  Swimlane Diagram (BPMN / UML)
  
The process will be organized into six swimlanes, each representing one of the above entities. This visually distinguishes responsibilities and shows clear hand-offs and data flows across departments and agencies.


![BPMN_DIAGRAM](https://github.com/user-attachments/assets/80283c43-1099-42db-a8ed-7ba5cb4dcdce)

Lane 1: Sensor System

Lane 2: Weather API

Lane 3: Oracle Database

Lane 4: Prediction Engine

Lane 5: Wildlife Officer

Lane 6: Disaster Team

Lane 7: MIS Dashboard

### Key BPMN Elements:

Start (hawk enters danger zone)

Tasks: Data collection → Data storage → Prediction → Validation → Alert → Dashboard update

Gateways: Disaster Detected? → Prediction Confirmed?

End: Alert delivered and logged

 
### ✅ 4. Brief Explanation (One Page)
### Business Process Explanation
This model represents an MIS-supported business process for tracking and forecasting hawk movements during disasters. The process begins when hawks enter a potential disaster-affected area. The Sensor System gathers location data, while the Weather API feeds live environmental conditions. All inputs are stored in the Oracle PL/SQL database, forming a centralized information system.

The Prediction Engine applies logic and analytics to forecast hawk movement patterns, identifying high-risk zones. This data is sent to a Wildlife Officer, who reviews and authorizes alerts. If validated, an alert is issued to the Disaster Response Unit, and all interactions are visualized through the MIS Dashboard.

The process supports core MIS functions:

Improves decision-making through accurate predictions.

Streamlines operations with automation.

Supports collaboration between departments.

Maintains historical data for future improvements.

This process is crucial for enhancing wildlife conservation during emergencies and aligning environmental protection with disaster management strategies.


------------------------
PHASE III
------------------------



### 1. Entity-Relationship (ER) Model
Entities and Attributes
### Disaster

disaster_id (PK, INTEGER)

disaster_type (VARCHAR)

severity_level (VARCHAR)

disaster_date (DATE)

location_id (FK, INTEGER)

### Location

location_id (PK, INTEGER)

region_name (VARCHAR)

latitude (NUMBER)

longitude (NUMBER)

### Hawk

hawk_id (PK, INTEGER)

species (VARCHAR)

tag_id (VARCHAR UNIQUE)

gender (VARCHAR)

age (NUMBER)

### Movement

movement_id (PK, INTEGER)

hawk_id (FK, INTEGER)

timestamp (TIMESTAMP)

location_id (FK, INTEGER)

altitude (NUMBER)

speed (NUMBER)

### Prediction

prediction_id (PK, INTEGER)

hawk_id (FK, INTEGER)

predicted_location_id (FK, INTEGER)

predicted_timestamp (TIMESTAMP)

confidence_level (NUMBER)

### Weather

weather_id (PK, INTEGER)

location_id (FK, INTEGER)

timestamp (TIMESTAMP)

temperature (NUMBER)

humidity (NUMBER)

wind_speed (NUMBER)



### The ER diagram will show the types of relationships:


<img width="773" alt="ER diagram" src="https://github.com/user-attachments/assets/6205d800-8f11-4d94-ac59-15cbaf278bc8" />

### 2. Relationships & Constraints
### One-to-Many:

One Location can be associated with many Disasters.

One Hawk can have many Movements.

One Hawk can have many Predictions.

One Location can have many Weather records.

### Many-to-One:

Many Movements refer to one Location.

Many Predictions refer to one Location.

### Constraints:

NOT NULL on all primary and foreign key fields.

UNIQUE constraint on Hawk tag_id.

CHECK constraints on values like severity_level and confidence_level (e.g., between 0–100).

DEFAULT values for timestamp (e.g., SYSDATE).
### 3 Normalization Check
1NF: All attributes have atomic values.

2NF: Non-key attributes depend on the whole primary key.

3NF: No transitive dependencies — attributes depend only on the primary key.

### 4. Real-World Data Scenarios Coverage
Supports tracking hawk movements and overlaying them with real-time disaster and weather data.

Predictive modeling for hawk migration with confidence intervals.

Disaster-based analysis using location-based filtering and weather impact.



---------------------------------------------
PHASE IV CREATING AND NAMING THE DATABASE
---------------------------------------------



🔖 Covers: Physical DB creation, user access, naming conventions, Oracle OEM setup, GitHub documentation

🎯 Objective
This phase focuses on building the physical environment for the system designed in Phases I–III. Using Oracle PL/SQL, we establish a named pluggable database, manage user roles, and prepare for monitoring and reporting via Oracle Enterprise Manager (OEM). This foundation allows the logical model to be executed in a real database environment.

🔨Database Creation
The Pluggable Database (PDB) was created using the following naming format:

Database Name: wed_26945_anitha_hawks_predictiona_analytics_db
Username: anitha

Password: anitha

Steps Executed in SQL Command Prompt

1.Create a pluggable database:
```sql
CREATE PLUGGABLE DATABASE WED_26945_Anitha_hawksprediction_pd
  ADMIN USER = anitha_admin IDENTIFIED BY anitha
  FILE_NAME_CONVERT (
    'C:\APP\ANITHA\PRODUCT\21C\ORADATA\XE\PDBSEED\',
    'C:\APP\ANITHA\PRODUCT\21C\ORADATA\XE\WED_26945_Anitha_hawksprediction_db\'
  );

```

Pluggable database created.
<img width="891" alt="PDB" src="https://github.com/user-attachments/assets/69d73ac6-7f37-4fa7-b79c-c168b8a47966" />

2.Open the newly created PDB:

```sql

ALTER PLUGGABLE DATABASE WED_26945_Anitha_hawksprediction_pd OPEN;

```
Pluggable database altered.

Use Makes the PDB ready for operations.

3.save the newly created PDB.

```sql
SQL> ALTER PLUGGABLE DATABASE wed_26687_gloria_online_retail_db SAVE STATE;
```
Pluggable database altered.

Use It makes sure that the PDB remains open after the database restarts.
4. Set the Session Container
```sql
SQL> ALTER SESSION SET CONTAINER = wed_26945_anitha_hawks_prediction_db;
```
Session altered.

Use: It changes the session to the newly created PDB for subsequent operations.
5.User Creation and Privilege Assignment
Create a Database User
```sql
SQL> create user anitha identified by anitha;
```
User created.

Use: It creates a new user, anitha, with the password anitha.
Grant Basic Privileges
```sql
SQL> GRANT CONNECT, RESOURCE, DBA, SYSDBA TO anitha;
```
Grant succeeded.
Use: To assigns full privileges for database operations.

  <img width="662" alt="pdbs" src="https://github.com/user-attachments/assets/85a06a6d-7c38-40a2-97c8-8c447bc62126" />
<img width="551" alt="pdbss" src="https://github.com/user-attachments/assets/e9728046-ad9c-43df-87e3-c776acf036ac" />

### Oracle Enterprise Manager (OEM) Setup 
### OEM URL to Access:
```sql
http://localhost:8080/em
```
<img width="944" alt="OEM" src="https://github.com/user-attachments/assets/675c35e5-cd05-4e51-a928-502b15ca81ef" />

----------------------------------------------------
PHASE V: TABLE IMPLEMENTATION AND DATA INSERTION
----------------------------------------------------


Phase Five focuses on implementing the physical structure of the Hawk Prediction Analytics database within Oracle and populating it with meaningful data. The goal is to transform the logical design created in earlier phases into a fully functional database that supports real-world queries and analytical operations, while maintaining data integrity.

### Table Creation
The database WED_26945_Anitha includes all the required tables aligned with the project scope. These tables are:

#### Location
```sql
CREATE TABLE Location (
    Location_ID INT PRIMARY KEY,
    Country VARCHAR2(50) NOT NULL,
    State VARCHAR2(50),
    City VARCHAR2(50)
);
```
#### Disaster

```sql
CREATE TABLE Disaster (
    Disaster_ID INT PRIMARY KEY,
    Disaster_Type VARCHAR2(50) NOT NULL,
    Date DATE NOT NULL,
    Magnitude DECIMAL(4,2),
    Location_ID INT,
    FOREIGN KEY (Location_ID) REFERENCES Location(Location_ID)
);
```

#### Weather_Conditions
```sql
CREATE TABLE Weather_Conditions (
    Condition_ID INT PRIMARY KEY,
    Location_ID INT,
    Temperature DECIMAL(5,2),
    Rainfall DECIMAL(5,2) DEFAULT 0,
    FOREIGN KEY (Location_ID) REFERENCES Location(Location_ID)
);
```
#### Prediction
```sql

CREATE TABLE Predictions (
    Prediction_ID INT PRIMARY KEY,
    Disaster_Type VARCHAR2(50),
    Predicted_Date DATE NOT NULL,
    Risk_Level VARCHAR2(10),
    Prediction_Method VARCHAR2(100),
    Predicted_Location_ID INT,
    FOREIGN KEY (Predicted_Location_ID) REFERENCES Location(Location_ID),
    CHECK (Risk_Level IN ('Low', 'Medium', 'High'))
);
```
#### Hawk_Movement

```sql

CREATE TABLE Hawk_Movement (
    Movement_ID INT PRIMARY KEY,
    Prediction_ID INT,
    Region VARCHAR2(100),
    Flight_Direction VARCHAR2(50),
    Distance_Migrated DECIMAL(6,2),
    Timestamp DATE,
    FOREIGN KEY (Prediction_ID) REFERENCES Predictions(Prediction_ID)
);
```
###  Data Insertion
Each table was populated with five realistic data entries, based on environmental and ecological data relevant to Rwanda, where various disasters and hawk movement patterns were recorded. This inserted data reflects typical use cases described in Phase One and supports predictive modeling for disaster response and ecological tracking.

### insert into location
```sql
INSERT INTO Location (Location_ID, Country, State, City)
VALUES (201, 'Rwanda', 'Kigali City', 'Kigali');

INSERT INTO Location (Location_ID, Country, State, City)
VALUES (202, 'Rwanda', 'Northern Province', 'Musanze');

INSERT INTO Location (Location_ID, Country, State, City)
VALUES (203, 'Rwanda', 'Western Province', 'Rubavu');

INSERT INTO Location (Location_ID, Country, State, City)
VALUES (204, 'Rwanda', 'Eastern Province', 'Rwamagana');

INSERT INTO Location (Location_ID, Country, State, City)
VALUES (205, 'Rwanda', 'Southern Province', 'Huye');

```
<img width="686" alt="location" src="https://github.com/user-attachments/assets/8cd3045a-8f20-4603-9987-5d980258c5e5" />


### insert into disaster
```sql
INSERT INTO Disaster VALUES (301, 'Flood', TO_DATE('2023-03-12', 'YYYY-MM-DD'), 4.2, 201);
INSERT INTO Disaster VALUES (302, 'Landslide', TO_DATE('2022-11-05', 'YYYY-MM-DD'), 3.8, 202);
INSERT INTO Disaster VALUES (303, 'Storm', TO_DATE('2023-08-21', 'YYYY-MM-DD'), 5.0, 203);
INSERT INTO Disaster VALUES (304, 'Heavy Rainfall', TO_DATE('2023-12-10', 'YYYY-MM-DD'), 4.7, 204);
INSERT INTO Disaster VALUES (305, 'Earthquake', TO_DATE('2024-02-18', 'YYYY-MM-DD'), 5.3, 205);
 

```
<img width="719" alt="ttt" src="https://github.com/user-attachments/assets/fb7650ef-51fb-4a66-9798-f5bb4e397628" />

### insert into prediction
```sql
INSERT INTO Predictions VALUES (501, 'Flood', TO_DATE('2024-05-10', 'YYYY-MM-DD'), 'High', 'Rainfall Forecast Model', 201);
INSERT INTO Predictions VALUES (502, 'Landslide', TO_DATE('2024-06-15', 'YYYY-MM-DD'), 'Medium', 'Soil Saturation Index', 202);
INSERT INTO Predictions VALUES (503, 'Storm', TO_DATE('2024-07-20', 'YYYY-MM-DD'), 'High', 'Wind Speed Trend Analysis', 203);
INSERT INTO Predictions VALUES (504, 'Heavy Rainfall', TO_DATE('2024-08-25', 'YYYY-MM-DD'), 'Medium', 'Radar Data Pattern', 204);
INSERT INTO Predictions VALUES (505, 'Earthquake', TO_DATE('2024-09-30', 'YYYY-MM-DD'), 'Low', 'Seismic History Mapping', 205);
```
<img width="814" alt="prediction" src="https://github.com/user-attachments/assets/d5f425dc-79c8-44ce-aa31-454b45092b05" />

### insert into weather condition 
```sql
INSERT INTO Weather_Conditions VALUES (401, 201, 22.5, 140.0);
INSERT INTO Weather_Conditions VALUES (402, 202, 20.8, 110.3);
INSERT INTO Weather_Conditions VALUES (403, 203, 23.1, 90.7);
INSERT INTO Weather_Conditions VALUES (404, 204, 24.0, 130.2);
INSERT INTO Weather_Conditions VALUES (405, 205, 21.7, 125.5);
```
<img width="825" alt="weather_condition" src="https://github.com/user-attachments/assets/319bb64b-0bee-4bd5-b0f4-24f8491c869c" />

#### insert into hawk_movement
```sql
INSERT INTO Hawk_Movement VALUES (601, 501, 'Nyungwe Forest', 'West', 112.5, TO_DATE('2024-05-11 08:00:00', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO Hawk_Movement VALUES (602, 502, 'Volcanoes Park', 'Northwest', 98.3, TO_DATE('2024-06-16 09:30:00', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO Hawk_Movement VALUES (603, 503, 'Akagera Wetlands', 'East', 125.0, TO_DATE('2024-07-21 07:15:00', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO Hawk_Movement VALUES (604, 504, 'Gishwati Reserve', 'Southwest', 87.4, TO_DATE('2024-08-26 10:45:00', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO Hawk_Movement VALUES (605, 505, 'Huye Highlands', 'South', 102.8, TO_DATE('2024-10-01 06:00:00', 'YYYY-MM-DD HH24:MI:SS'));
```

<img width="831" alt="hawks movement" src="https://github.com/user-attachments/assets/d4efe813-0548-4397-8ce2-d1158e1e8022" />

## Data Integrity
To guarantee consistency, accuracy, and validity of data throughout the system, the following practices were implemented:

### Referential Integrity:

All FOREIGN KEY constraints ensure that dependent tables (e.g., Disaster, Predictions, Hawk_Movement) only accept valid references from primary tables (Location, Predictions).

### Check Constraints:

The Risk_Level in the Predictions table uses a CHECK constraint to allow only 'Low', 'Medium', or 'High'.

NOT NULL Constraints:

Primary key and essential fields (like Country, Predicted_Date, etc.) were declared NOT NULL to avoid missing values.
Unique Identifiers:

Each table includes unique ID columns (e.g., Location_ID, Prediction_ID) for unambiguous record identification.
Data Validation Queries:

Joined queries were tested to confirm relational accuracy (e.g., INNER JOIN between Hawk_Movement and Predictions only returns matching data).

### Example validation query:
```sql
SELECT h.Movement_ID, h.Region, p.Risk_Level
FROM Hawk_Movement h
JOIN Predictions p ON h.Prediction_ID = p.Prediction_ID;
```


### Physical Database Structure
The physical structure of the database was built directly from the logical model created in Phase Three, with enhancements to ensure optimal storage, relationships, and indexing support for query operations.

### Appropriate Data Types:

NUMBER used for identifiers and magnitudes

VARCHAR2 used for names, directions, and region fields

DATE and TIMESTAMP used for disaster dates and movement tracking


### Primary Keys and Foreign Keys:

Every table includes a clearly defined PRIMARY KEY (e.g., Location_ID, Disaster_ID, Prediction_ID)

Foreign keys are defined to connect dependent data across tables, such as Location_ID in Disaster, and Prediction_ID in Hawk_Movement

Constraints for Data Validity:

NOT NULL constraints enforce required values (e.g., Country, Predicted_Date)

CHECK constraints on columns like Risk_Level to limit acceptable values

UNIQUE constraints ensure identifiers are not duplicated

### Indexing:

Indexes may be added on frequently joined or searched columns like Prediction_ID, Location_ID for performance enhancement



### PHASE IV:  Database Interaction and Transactions 

DDL Operations:
```sql

ALTER TABLE Hawk_Movement ADD Wind_Speed NUMBER(5,2);
```
 DML Operations:
 ```sql

INSERT INTO Hawk_Movement VALUES (
   606, 501, 'Nyabarongo Swamp', 'South', 110.5, TO_DATE('2024-05-12 09:00:00', 'YYYY-MM-DD HH24:MI:SS'), 18.6
);


UPDATE Predictions SET Prediction_Method = 'Updated Forecast Model' WHERE Prediction_ID = 501;


DELETE FROM Weather_Conditions WHERE Condition_ID = 405;
```
### Problem Statement for Analytics
 Use of Window Functions:
 ```sql
SELECT 
    p.Disaster_Type,
    p.Risk_Level,
    h.Region,
    h.Distance_Migrated,
    RANK() OVER (PARTITION BY p.Disaster_Type ORDER BY h.Distance_Migrated DESC) AS Distance_Rank
FROM 
    Hawk_Movement h
JOIN 
    Predictions p ON h.Prediction_ID = p.Prediction_ID;
```
<img width="844" alt="window function" src="https://github.com/user-attachments/assets/1479e97c-8ab8-4ae2-9b4f-c5f947d51406" />

###  Procedures and Functions
```sql
CREATE OR REPLACE PROCEDURE Get_Hawk_By_Risk (
    risk IN VARCHAR2
) AS
BEGIN
    FOR rec IN (
        SELECT h.Region, h.Distance_Migrated, p.Risk_Level
        FROM Hawk_Movement h
        JOIN Predictions p ON h.Prediction_ID = p.Prediction_ID
        WHERE p.Risk_Level = risk
    ) LOOP
        DBMS_OUTPUT.PUT_LINE('Region: ' || rec.Region || ' | Distance: ' || rec.Distance_Migrated);
    END LOOP;
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
<img width="835" alt="procedure" src="https://github.com/user-attachments/assets/43ed4aec-c478-4df8-ab48-45e5515ee3da" />

```
### Testing and Validation
```sql
BEGIN
  HawkAnalytics.Get_Hawk_By_Risk('High');
END;

```
### Test the Function
```sql
SELECT Total_Migration(501) AS Total_Distance FROM dual;
```
### Packages

```sql
CREATE OR REPLACE PACKAGE HawkAnalytics AS
    PROCEDURE Get_Hawk_By_Risk(risk IN VARCHAR2);
    FUNCTION Total_Migration(pred_id IN NUMBER) RETURN NUMBER;
END HawkAnalytics;
```
### package body
```sql
CREATE OR REPLACE PACKAGE BODY HawkAnalytics AS
    PROCEDURE Get_Hawk_By_Risk(risk IN VARCHAR2) IS
    BEGIN
        FOR rec IN (
            SELECT h.Region, h.Distance_Migrated, p.Risk_Level
            FROM Hawk_Movement h
            JOIN Predictions p ON h.Prediction_ID = p.Prediction_ID
            WHERE p.Risk_Level = risk
        ) LOOP
            DBMS_OUTPUT.PUT_LINE('Region: ' || rec.Region || ' | Distance: ' || rec.Distance_Migrated);
        END LOOP;
    EXCEPTION
        WHEN OTHERS THEN
            DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
    END;

    FUNCTION Total_Migration(pred_id IN NUMBER) RETURN NUMBER IS
        total NUMBER;
    BEGIN
        SELECT SUM(Distance_Migrated)
        INTO total
        FROM Hawk_Movement
        WHERE Prediction_ID = pred_id;
        
        RETURN total;
    EXCEPTION
        WHEN NO_DATA_FOUND THEN RETURN 0;
        WHEN OTHERS THEN RETURN -1;
    END;

END HawkAnalytics;
```


### PHASE VII


The Hawk Prediction Analytics system processes real-time ecological and weather data to predict hawk behavior during disasters. However, unauthorized or ill-timed updates to the prediction and migration records could compromise data accuracy. To address this, advanced PL/SQL features such as triggers and auditing mechanisms are required to enforce timing restrictions and track all modification attempts for sensitive tables.

 ### Justification for Triggers, Packages, and Auditing:
Triggers are required to restrict INSERT, UPDATE, and DELETE operations during weekdays and public holidays.

Packages automate logic to check date conditions and log actions.

Auditing ensures traceability of all user interactions with the system for accountability

### Restriction Rule:
Block DML operations (INSERT, UPDATE, DELETE) from Monday to Friday

Block all such activity on public holidays listed in a holiday reference table for the upcoming month

 ### Trigger Implementation
 ```sql
CREATE TABLE Public_Holidays (
    Holiday_Date DATE PRIMARY KEY,
    Description VARCHAR2(100)
);
```
### Simple BEFORE INSERT Trigger (example for Hawk_Movement)
```sql
CREATE OR REPLACE TRIGGER trg_block_weekday_inserts
BEFORE INSERT OR UPDATE OR DELETE ON Hawk_Movement
FOR EACH ROW
DECLARE
    v_day VARCHAR2(10);
    v_today DATE := TRUNC(SYSDATE);
    v_count NUMBER;
BEGIN
    -- Get the day name
    SELECT TO_CHAR(v_today, 'DY') INTO v_day FROM dual;

    -- Check if today is in holiday list
    SELECT COUNT(*) INTO v_count
    FROM Public_Holidays
    WHERE Holiday_Date = v_today;

    -- Block if it's a weekday (Mon–Fri) or holiday
    IF v_day IN ('MON', 'TUE', 'WED', 'THU', 'FRI') OR v_count > 0 THEN
        RAISE_APPLICATION_ERROR(-20001, 'Modifications not allowed on weekdays or holidays.');
    END IF;
END;
```
### Compound Trigger (for complex insert logging)
```sql
CREATE OR REPLACE TRIGGER trg_audit_hawk_movement
FOR INSERT OR UPDATE OR DELETE ON Hawk_Movement
COMPOUND TRIGGER
    -- Variables to collect audit details
    TYPE t_audit IS TABLE OF VARCHAR2(500) INDEX BY PLS_INTEGER;
    v_log t_audit;
    i INTEGER := 0;

AFTER EACH ROW IS
BEGIN
    i := i + 1;
    v_log(i) := USER || ' performed ' || ORA_SYSEVENT || 
                ' on Hawk_Movement at ' || TO_CHAR(SYSDATE, 'DD-MON-YYYY HH24:MI:SS');
END AFTER EACH ROW;

AFTER STATEMENT IS
BEGIN
    FOR j IN 1..v_log.COUNT LOOP
        INSERT INTO Audit_Log (User_ID, Action_Time, Operation, Status)
        VALUES (USER, SYSDATE, v_log(j), 'Allowed');
    END LOOP;
END AFTER STATEMENT;

END trg_audit_hawk_movement;
```

### ✅  Auditing with Restrictions and Tracking
### 🗂️ Audit Table:
```sql
CREATE TABLE Audit_Log (
    Log_ID NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    User_ID VARCHAR2(50),
    Action_Time TIMESTAMP,
    Operation VARCHAR2(200),
    Status VARCHAR2(20)
);
```

### 📦 Audit Utility Package:
#### package specification
```sql
CREATE OR REPLACE PACKAGE Audit_Utils AS
  FUNCTION Is_Restricted RETURN BOOLEAN;
  PROCEDURE Log_Action(op VARCHAR2, stat VARCHAR2);
END Audit_Utils;
```

#### Package Body:
```sql
CREATE OR REPLACE PACKAGE BODY Audit_Utils AS

  FUNCTION Is_Restricted RETURN BOOLEAN IS
    v_day VARCHAR2(10);
    v_count NUMBER;
  BEGIN
    SELECT TO_CHAR(SYSDATE, 'DY', 'NLS_DATE_LANGUAGE=ENGLISH') INTO v_day FROM dual;

    SELECT COUNT(*) INTO v_count
    FROM Public_Holidays
    WHERE Holiday_Date = TRUNC(SYSDATE)
      AND Holiday_Date BETWEEN TRUNC(SYSDATE) AND LAST_DAY(ADD_MONTHS(SYSDATE, 1));

    RETURN (v_day IN ('MON', 'TUE', 'WED', 'THU', 'FRI') OR v_count > 0);
  END;

  PROCEDURE Log_Action(op VARCHAR2, stat VARCHAR2) IS
  BEGIN
    INSERT INTO Audit_Log (User_ID, Action_Time, Operation, Status)
    VALUES (USER, SYSTIMESTAMP, op, stat);
  END;

END Audit_Utils;
```

### ✅ Security & System Alignment
This solution enhances the project’s security, data governance, and trustworthiness by:

 Preventing destructive actions during restricted times

 Tracking user behavior with full visibility

 Automating enforcement using modular, reusable code

 Supporting MIS objectives by ensuring reliability in operational data


