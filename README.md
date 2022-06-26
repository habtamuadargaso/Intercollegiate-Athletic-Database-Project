# Intercollegiate-Athletic-Database
The IntercollegiateAthleticDatabaseis an MYSQL relational database for the intercollegiate
to support the scheduling and operation of the event. It contains eight tables: categories ,
Employee, Customer, Facility,Location, ResourceTbl,EventRequest,
EventPlan,EventPlanLine. The EventRequesttableis the hub of the database. An event
request represents an event scheduled at a facility. For example, a basketball game may be
scheduled at the gymnasium. Events are sometimes scheduled several months in advance.
Holding an event requires resources including personnel and equipment. Resources are assigned
to specific locations of a facility. For example, guards may be required at the gates of the football
stadium. The EventPlan table defines a plan for the setup, operation, and cleanup of an event.
The EventPlanLine table contains the individual resources required in an event plan.


# Creat Table 1 Customer
```
use InterCollegiateAthleticDatabase;
DROP DATABASE IF EXISTS InterCollegiateAthleticDatabase;
CREATE TABLE Customer
(CustNo VARCHAR(8) NOT NULL COMMENT 'Customer number',
CustName VARCHAR(30) NOT NULL COMMENT 'Customer name',
Address VARCHAR(50) NOT NULL COMMENT 'Customer address',
Internal CHAR(1) NOT NULL COMMENT 'Customer type (Yes if internal, No otherwise)',
Contact VARCHAR(35) NOT NULL COMMENT 'Contact person',
Phone VARCHAR(11) NOT NULL COMMENT 'Contact phone number',
City VARCHAR(30) NOT NULL COMMENT 'City',
State VARCHAR(2) NOT NULL COMMENT 'State',
Zip VARCHAR(10) NOT NULL COMMENT 'Zip code',
CONSTRAINT PK_CUSTOMER PRIMARY KEY (CustNo) ) ;
```
