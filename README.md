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


# Create Table 1 Customer
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
# Create Table 2 Facility
```
CREATE TABLE Facility
(FacNo VARCHAR(8) NOT NULL COMMENT 'Facility number',
FacName VARCHAR(30) NOT NULL COMMENT 'Facility name',
CONSTRAINT PK_FACILITY PRIMARY KEY (FacNo) );
```


# Create Table 3 Location
```
CREATE TABLE Location
(LocNo VARCHAR(8) NOT NULL COMMENT 'Location number',
FacNo VARCHAR(8) NOT NULL COMMENT 'Facility number',
LocName VARCHAR(30) NOT NULL COMMENT 'Location name',
CONSTRAINT PK_LOCATION PRIMARY KEY (LocNo),
CONSTRAINT FK_FACNO FOREIGN KEY (FacNo) REFERENCES FACILITY (FacNo) );

```

# Create Table 4 Employee
```
CREATE TABLE Employee
(EmpNo VARCHAR(8) NOT NULL COMMENT 'Employee number',
EmpName VARCHAR(35) NOT NULL COMMENT 'Employee name',
Department VARCHAR(25) NOT NULL COMMENT 'Department',
Email VARCHAR(30) NOT NULL COMMENT 'electronic mail address',
Phone VARCHAR(10) NOT NULL,
CONSTRAINT PK_EMPLOYEE PRIMARY KEY (EmpNo) ) ;

```
# Create Table 5 ResourcelTbl
```
CREATE TABLE ResourceTbl
(ResNo VARCHAR(8) NOT NULL,
ResName VARCHAR(30) NOT NULL,
Rate DECIMAL(15,4) NOT NULL CHECK (Rate > 0),
CONSTRAINT PK_RESOURCE PRIMARY KEY (ResNo) ) COMMENT 'ORIGINAL NAME:Resource';
```
# Create Table 6 EventRequest
```
CREATE TABLE EventRequest
(EventNo VARCHAR(8) NOT NULL COMMENT 'Event number',
DateHeld DATE NOT NULL COMMENT 'Event date',
DateReq DATE NOT NULL COMMENT 'Date requested',
CustNo VARCHAR(8) NOT NULL COMMENT 'Customer number',
FacNo VARCHAR(8) NOT NULL COMMENT 'Facility number',
DateAuth DATE COMMENT 'Date authorized',
Status VARCHAR(20) NOT NULL COMMENT 'Status of event request' CHECK (Status IN ('Pending', 'Denied',
'Approved')),
EstCost DECIMAL(15,4) NOT NULL COMMENT 'Estimated cost',
EstAudience DECIMAL(11,0) NOT NULL COMMENT 'Estimated audience' CHECK (EstAudience > 0),
BudNo VARCHAR(8) COMMENT 'Budget number',
CONSTRAINT PK_EVENTREQUEST PRIMARY KEY (EventNo),
CONSTRAINT FK_EVENT_FACNO FOREIGN KEY (FacNo) REFERENCES FACILITY (FacNo),
CONSTRAINT FK_CUSTNO FOREIGN KEY (CustNo) REFERENCES CUSTOMER (CustNo) );
```

# Create Table 7 EventPlan
```
CREATE TABLE EventPlan
(PlanNo VARCHAR(8) NOT NULL COMMENT 'Event plan number',
EventNo VARCHAR(8) NOT NULL COMMENT 'Event number',
WorkDate DATE NOT NULL COMMENT 'Work date',
Notes VARCHAR(50),
Activity VARCHAR(50) NOT NULL,
EmpNo VARCHAR(8),
CONSTRAINT PK_EVENTPLAN PRIMARY KEY (PlanNo),
CONSTRAINT FK_EMPNO FOREIGN KEY (EmpNo) REFERENCES EMPLOYEE (EmpNo),
CONSTRAINT FK_EVENTNO FOREIGN KEY (EventNo) REFERENCES EVENTREQUEST (EventNo) );
```
# Create Table 8 EventPlanline

```

drop table EventPlanline;
CREATE TABLE EventPlanLine
(PlanNo VARCHAR(8) NOT NULL COMMENT 'Event Event plan number',
LineNo INTEGER NOT NULL COMMENT 'line number',
TimeStart datetime NOT NULL COMMENT 'Time start',
TimeEnd DATEtime NOT NULL COMMENT 'Time end',
NumberFld INTEGER NOT NULL COMMENT 'ORIGINAL NAME:number , Number of resources needed',
LocNo VARCHAR(8) NOT NULL,
ResNo VARCHAR(8) NOT NULL,
 CHECK (TimeStart < TimeEnd), 
CONSTRAINT PK_EVENTPLANLINE PRIMARY KEY (PlanNo, LineNo),
CONSTRAINT FK_LOCNO FOREIGN KEY (LocNo) REFERENCES LOCATION (LocNo),
CONSTRAINT FK_RESNO FOREIGN KEY (ResNo) REFERENCES RESOURCETBL (ResNo),
CONSTRAINT FK_PLANNO FOREIGN KEY (PlanNo) REFERENCES EVENTPLAN (PlanNo) );
```




