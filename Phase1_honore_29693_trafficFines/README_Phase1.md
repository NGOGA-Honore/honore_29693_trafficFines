# Phase I – Business Process Modeling

## Project Title

**TrafficFineTrack: Traffic Violation, Fine Payment and Arrears Monitor**

## Student Information

|Field|Value|
|-|-|
|Student|NGOGA Honore|
|Student ID|29693|
|Course|INSY 8311, Database Development with PL/SQL|
|Instructor|Eric Maniraguha|
|Faculty|Faculty of Information Technology (AUCA)|
|Academic Year|2026–2027, Semester I|
|Phase|Phase I: Business Process Modeling|

## 1\. Business Process Overview

TrafficFineTrack is an Oracle PL/SQL database system that manages traffic violations, fines, payments, arrears, and repeat offenders. The system ensures that each violation is recorded once, every citation generates a corresponding fine, each payment is linked to a fine, and overdue cases can be detected and reported.

The business process starts when a traffic officer records a violation. If the violation is a **warning**, the system stores the record without creating a fine. If the violation is a **citation**, the system creates a fine, sets a due date, and tracks the amount owed. A cashier or authorized staff member may later record a payment against the fine. The database enforces business rules so that duplicate tickets, overpayments, and unauthorized edits to payment history are blocked.

## 2\. Main Business Actors

|Actor|Role in the process|
|-|-|
|Traffic Officer|Records violation details at the time of the incident|
|Cashier / Finance Clerk|Records payment for an issued fine|
|Database System|Validates business rules, stores transactions, and updates status|
|Supervisor / Manager|Reviews arrears, repeat offenders, and audit logs|

## 3\. Business Rules

1. Every violation must be linked to a vehicle and a violation type.
2. Only violations classified as **citation** generate fines.
3. A fine must have a due date based on the issue date and configured grace period.
4. Payments cannot exceed the remaining balance of a fine.
5. A paid fine cannot be paid again.
6. Duplicate tickets for the same vehicle, charge, date, and time must be blocked.
7. Payment history cannot be edited or deleted without authorization.
8. Overdue fines must be identified and reported.
9. Repeat offenders are detected based on the number of violations in a rolling 12-month period.
10. Every important change must be recorded in an audit log.

## 4\. Business Process Steps

### Step 1: Record a violation

* The traffic officer enters the date, time, location, vehicle information, and charge.
* The system checks whether the violation already exists.
* If it is a duplicate, the system rejects it.
* If valid, the violation is saved.

### Step 2: Decide whether the violation is a warning or citation

* If the violation is a warning, no fine is created.
* If the violation is a citation, the system creates a fine.

### Step 3: Generate a fine

* The system assigns a fine amount from the fine schedule.
* The system calculates the due date.
* The fine is marked as unpaid.

### Step 4: Record payment

* The cashier enters the fine reference and payment amount.
* The system checks the remaining balance.
* If the payment is valid, it is saved and the fine status is updated.
* If the payment exceeds the balance, the system rejects it.

### Step 5: Track overdue fines

* The system periodically checks unpaid fines past the due date.
* Overdue fines are added to the arrears report.
* Late surcharge may be applied according to the business rules.

### Step 6: Detect repeat offenders

* The system counts violations for each driver within the last 12 months.
* If the threshold is exceeded, the driver is marked as a repeat offender.

### Step 7: Audit and reporting

* Every insert/update on fines and payments is logged.
* Supervisors can review arrears, repeat offenders, and audit history.

## 5\. Inputs and Outputs

|Category|Examples|
|-|-|
|Inputs|violation date, time, location, vehicle data, charge, payment amount|
|Outputs|fine record, payment receipt, arrears report, repeat-offender list, audit log|

## 6\. Proposed Database Objects

|Object|Purpose|
|-|-|
|`driver`|Store generated driver records|
|`vehicle`|Store vehicle details|
|`violation\\\_type`|Store violation categories and fine schedule|
|`violation`|Store each violation event|
|`fine`|Store issued fines and due dates|
|`payment`|Store payments against fines|
|`system\\\_parameter`|Store configurable business rules|
|`audit\\\_log`|Store change history for accountability|

## 7\. Relationship Summary

* One driver can own many vehicles.
* One vehicle can have many violations.
* One violation type can be used in many violations.
* One citation violation creates one fine.
* One fine can receive one or more payments.
* Each fine and payment action is recorded in the audit log.

## 8\. Conclusion

This business process model shows how TrafficFineTrack manages the full life cycle of a traffic violation, from recording the incident to collecting payment and identifying arrears. The model provides a strong foundation for the Oracle database schema, PL/SQL procedures, triggers, and reports that will be developed in the next phases.

## 9\. Business Process Diagram Link

**https://app.diagrams.net/?utm\_source=.com#G17crFIOmPPHt9iC\_GMaIHvqLabNps9ytZ#%7B%22pageId%22%3A%22traffic-fine-monochrome%22%7D**

