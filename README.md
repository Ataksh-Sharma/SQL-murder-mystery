# SQL-murder-mystery

# SQL Crime Investigation Queries
This repository contains a collection of SQL queries crafted to solve a fictional crime investigation scenario. By analyzing data stored in relational tables, these queries aim to uncover critical evidence, identify suspects and witnesses, and reveal connections between individuals and events. The dataset includes tables such as `crime_scene_report`, `person`, `interview`, `drivers_license`, `get_fit_now_member`, `get_fit_now_check_in`, and `facebook_event_checkin`. 

This project demonstrates the practical application of SQL in problem-solving, particularly in the context of investigations and forensic analysis. By exploring these queries, users can improve their SQL skills, understand complex joins and subqueries, and appreciate how databases can aid in critical decision-making processes.

Each query is designed to answer specific investigative questions, utilizing advanced SQL techniques such as filtering, joins, subqueries, and pattern matching. The goal is to demonstrate how SQL can be effectively used in real-world problem-solving scenarios, particularly for forensic or investigative purposes.

-- Retrieve the report for a murder that occurred on January 15, 2018, in SQL City

SELECT *

FROM crime_scene_report

WHERE date = '20180115' AND type = 'murder' AND city = 'SQL City';

-- Identify the resident with the highest address number on Northwestern Dr

SELECT *

FROM person

WHERE address_street_name = 'Northwestern Dr' 

AND address_number = (SELECT MAX(address_number) FROM person);

-- Find all individuals with the name "Annabel" residing on Franklin Ave

SELECT *

FROM person

WHERE address_street_name = 'Franklin Ave' AND name LIKE '%Annabel%';

-- Fetch details of two specific individuals by their IDs

SELECT *

FROM person

WHERE id IN (14887, 16371);

-- Retrieve interview records for the two individuals identified earlier

SELECT *

FROM interview

WHERE person_id IN (14887, 16371);

-- Find Gold members with an ID starting with "48Z" who checked in on January 9, 2018

SELECT *

FROM get_fit_now_member AS g

JOIN get_fit_now_check_in AS g1

ON g.id = g1.membership_id

WHERE g.id LIKE '48Z%' AND g.membership_status = 'gold' AND g1.check_in_date = '20180109';

-- Find individuals associated with a vehicle having a plate number ending in "H42W"

SELECT *

FROM person AS P

JOIN drivers_license AS d

ON p.license_id = d.id

WHERE (p.id = 288119 OR p.id = 67318) AND (d.plate_number LIKE '%H42W%');

-- Retrieve the interview record for a suspect with ID 67318

SELECT *

FROM interview

WHERE person_id = 67318;

-- Identify a red-haired female Tesla Model S owner who attended the SQL Symphony Concert

SELECT p.name

FROM person AS p

JOIN drivers_license AS d 

ON p.license_id = d.id

JOIN facebook_event_checkin AS f

ON p.id = f.person_id

WHERE d.car_make = 'Tesla'

AND d.car_model = 'Model S'

AND d.hair_color = 'red'

AND d.gender = 'female'

AND f.event_name = 'SQL Symphony Concert';

### How to Use
**Setup the Database:** Ensure you have access to a relational database containing the necessary tables and data.

**Execute the Queries:** Copy and paste the SQL queries into your SQL client or database management tool to retrieve the required information.

**Analyze the Results:** Use the query outputs to draw connections, identify suspects or witnesses, and establish a timeline of events.
