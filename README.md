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

###insert into disaster
```sql
INSERT INTO Disaster VALUES (301, 'Flood', TO_DATE('2023-03-12', 'YYYY-MM-DD'), 4.2, 201);
INSERT INTO Disaster VALUES (302, 'Landslide', TO_DATE('2022-11-05', 'YYYY-MM-DD'), 3.8, 202);
INSERT INTO Disaster VALUES (303, 'Storm', TO_DATE('2023-08-21', 'YYYY-MM-DD'), 5.0, 203);
INSERT INTO Disaster VALUES (304, 'Heavy Rainfall', TO_DATE('2023-12-10', 'YYYY-MM-DD'), 4.7, 204);
INSERT INTO Disaster VALUES (305, 'Earthquake', TO_DATE('2024-02-18', 'YYYY-MM-DD'), 5.3, 205);
```

###insert into prediction
```sql
INSERT INTO Predictions VALUES (501, 'Flood', TO_DATE('2024-05-10', 'YYYY-MM-DD'), 'High', 'Rainfall Forecast Model', 201);
INSERT INTO Predictions VALUES (502, 'Landslide', TO_DATE('2024-06-15', 'YYYY-MM-DD'), 'Medium', 'Soil Saturation Index', 202);
INSERT INTO Predictions VALUES (503, 'Storm', TO_DATE('2024-07-20', 'YYYY-MM-DD'), 'High', 'Wind Speed Trend Analysis', 203);
INSERT INTO Predictions VALUES (504, 'Heavy Rainfall', TO_DATE('2024-08-25', 'YYYY-MM-DD'), 'Medium', 'Radar Data Pattern', 204);
INSERT INTO Predictions VALUES (505, 'Earthquake', TO_DATE('2024-09-30', 'YYYY-MM-DD'), 'Low', 'Seismic History Mapping', 205);

```
###insert into weather condition 
```sql
INSERT INTO Weather_Conditions VALUES (401, 201, 22.5, 140.0);
INSERT INTO Weather_Conditions VALUES (402, 202, 20.8, 110.3);
INSERT INTO Weather_Conditions VALUES (403, 203, 23.1, 90.7);
INSERT INTO Weather_Conditions VALUES (404, 204, 24.0, 130.2);
INSERT INTO Weather_Conditions VALUES (405, 205, 21.7, 125.5);
```
####insert into hawk_movement
```sql
INSERT INTO Hawk_Movement VALUES (601, 501, 'Nyungwe Forest', 'West', 112.5, TO_DATE('2024-05-11 08:00:00', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO Hawk_Movement VALUES (602, 502, 'Volcanoes Park', 'Northwest', 98.3, TO_DATE('2024-06-16 09:30:00', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO Hawk_Movement VALUES (603, 503, 'Akagera Wetlands', 'East', 125.0, TO_DATE('2024-07-21 07:15:00', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO Hawk_Movement VALUES (604, 504, 'Gishwati Reserve', 'Southwest', 87.4, TO_DATE('2024-08-26 10:45:00', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO Hawk_Movement VALUES (605, 505, 'Huye Highlands', 'South', 102.8, TO_DATE('2024-10-01 06:00:00', 'YYYY-MM-DD HH24:MI:SS'));
```

