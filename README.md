PHASE II
-----------------
 
 1. Define the Scope

Real-Time Disaster Management Information System (DMIS)

 Process Being Modeled
A system for collecting and processing real-time data to identify disasters and coordinate emergency responses across local and international agencies.

  OBJECTIVES

  
Process live environmental data (e.g., seismic activity, floods, fires).
Automatically detect disasters and trigger alerts.
Support informed decision-making via real-time dashboards.
Facilitate rapid coordination between emergency responders.
Enable international collaboration during cross-border disasters.


 Expected Outcomes


 
Automated early warning alerts to relevant authorities and the public.
Improved disaster preparedness and response.
Effective collaboration between national and international stakeholders.

   Identify Key Entities
   
Entity	Role & Responsibilities

Sensor Network	Collects real-time data from the environment (e.g., temperature, water levels, seismic activity).


MIS Core System	Aggregates, filters, and analyzes data; identifies potential disasters.


Disaster Alert System	Sends alerts to emergency responders, citizens, and government agencies.


Emergency Response Agency	Activates response plans, dispatches personnel and equipment, coordinates local rescue and relief.


Government Command Center	Makes strategic decisions, allocates national resources, manages public communication.


International Agencies	Receives shared data for cross-border response coordination and global disaster support.



  Use Swimlanes for Clarity
  
The process will be organized into six swimlanes, each representing one of the above entities. This visually distinguishes responsibilities and shows clear hand-offs and data flows across departments and agencies.

 Swimlane Layout (Top to Bottom):
Sensor Network

MIS Core System

Disaster Alert System

Emergency Response Agency

Government Command Center

International Agencies

  Apply UML/BPMN Notations
 Key BPMN Elements Used:
BPMN Symbol	Usage
 Start Event	Start of the data collection process
 Task	An activity such as "Collect Data", "Send Alert", or "Deploy Response Team"
 Gateway	A decision point (e.g., "Is threshold exceeded?")
 End Event	End of the disaster response process
 Sequence Flow	Arrows showing the order of tasks
Swimlanes	Represent different systems and entities involved


<img width="313" alt="BPMN Diagram" src="https://github.com/user-attachments/assets/5dd3ff7d-1765-444d-a09d-3a7e925a26be" />
 
One-Page Explanation


The BPMN diagram models the workflow of a Real-Time Disaster Management Information System (DMIS) designed to detect and respond to environmental disasters. It begins with data collection from a network of environmental sensors that stream live information to the system. The MIS Core System analyzes this data in real-time to detect anomalies that may indicate an impending disaster. If thresholds are exceeded, the system triggers alerts through the Disaster Alert System, which notifies Emergency Response Agencies and the Government Command Center. Emergency responders take swift action by deploying teams and equipment, while the government oversees the national response and makes strategic decisions. If the disaster is large-scale or cross-border, data is automatically shared with International Agencies for broader coordination and support. The system ensures fast, informed decision-making and allows for data-driven, collaborative disaster response. The swimlane structure ensures role clarity, and the logical flow maps all major decisions, responses, and data-sharing activities clearly and consistently, making this system a vital part of modern MIS for crisis management.










------------------------
PHASE III
------------------------




Logical Data Model Design
Entity Descriptions

Disaster: Tracks disaster details (e.g., type, magnitude, location).

Location: Stores geographical data (e.g., country, state, city).

Prediction: Logs disaster predictions (e.g., type, risk level).

Weather Condition: Records weather-related data (e.g., temperature, rainfall).

Preparedness Measure: Explains strategies against disasters.

Historical Disaster Data: Maintains past disaster history records.

Entity-Relationship Diagram (ERD)

The ER diagram will show the types of relationships:



One-to-many relationships between disasters and locations.
Many-to-one relationships between predictions and locations.
Many-to-many relationships between historical data, disasters, and locations.


---------------------------------------------
PHASE IV CREATING AND NAMING THE DATABASE
---------------------------------------------
Username: wed_26945_anitha_hawksprediction
password: anitha
Physical Database structure
1. tables created : location, disaster, prediction, hawk_movement, weather_condition
2.  Relationshps: the tables are related with foreign key to maintain referential intergrity.
3.  constraints: primary keys , foreign keys, and unique  keys are imposed




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

### insert into loacation
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



