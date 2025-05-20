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











PHASE III
-----------




Logical Data Model Design
Entity Descriptions

Disaster: Tracks disaster details (e.g., type, magnitude, location).

Location: Stores geographical data (e.g., country, state, city).

Prediction: Logs disaster predictions (e.g., type, risk level).

Weather Condition: Records weather-related data (e.g., temperature, rainfall).

Preparedness Measure: Explains strategies against disasters.

Historical Disaster Data: Maintains past disaster history records.

Entity-Relationship Diagram (ERD)

The ER diagram will map the following types of relationships:



One-to-many relationships between disasters and locations.
Many-to-one relationships between predictions and locations.
Many-to-many relationships between historical data, disasters, and locations.




