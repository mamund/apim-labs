# Request for Vehicle Service (RVS)

## Purpose
We use the Request for Vehicle Service (RVS) process to manage customer requests for maintainence of thier vehicle.

## Actions
There are two personas for the RVS process: Customers and Service Staff.

Customers can create a new RVS record, update an exsiting RVS (if status is set to `pending`), cancel an existing  RVS (if status is set to `pending`), and list existing  RVS records (including filtering by date, vehicle ID, and status)

Service Staff can update an existing RVS record, assign a Customer (via CID) to an existing RVS record, assign one or more Service staff members (via SIDs) to an existing RVS record, change the status of an existing RVS record (pending, working, completed, cancelled), attach one or more existing Service Work Records (via WIDs) to an existing RVS record.

## Data
An RVS record consists of the following data properties:
* RID (RVS identifier)
* CID (Customer identifier)
* VIN (Vehicle identification number)
* SID (Service Staff identifier)  more than one SID can be attached
* WID (Service Work Record) more then one WID can be attached
* Customer Name (open text, resolved against CID)
* Requested Work (open text, multi-line)
* Status (`pending`, `working`, `completed`, `cancelled`) defaults to pending
* Service Notes (open text, mult-line) for Service Staff comments
* DateCreated
* DateUpdated

### Notes
* RID is generated when the record is created
* CID is added after the customer creates the record. Initially, customer only adds their name.
* VIN is standardized data point (NHTSA, 1954)
* SID is a pointer to an existing Service Staff record. More than one SID can be attached to an exisitng RVS. 
* WID is a pointer to an existing Service Work Record created by Service staff. More than one WID can be attached to an existing RVS.
* Customer Name is open-text field filled in by customer, updated by Service Staff
* Requested work is open-text, multi-line field filled in by customer
* Status is set to `pending` when RVS is created. It is modified by Service staff (`working`, `completed`, `cancelled`). Customers can mark a `pending` record as `cancelled`.
* DateCreated is the UTC date/time the RVS was first created
* DateUpdated is the UTC date/time the RVS as modifed in any way

### Customer Record (CR)
The CID belongs to the Customer Record (CR). Manageing CRs is a separate process covered elsewhere in this documentation.

### Service Staff Record (SSR)
The SID belongs to the Service Staff Record (SSR). Manging SSRs is a separate process covered elsewhere in this documentaiton.

### Service Work Record (SWR)
The WID belongs to the Service Work Record (SWR). Managing SWRs is a separate process covered elsewhere in this documentation. 

## Other Considerations
* Listing RVS records should support paging (`first`, `previous`, `next`, `last`).
* Filtering the list of RVS records support support:
  * DateCreated (UTC)
  * VIN (portion)
  * CID (portion) - Service Staff only
  * Status (`pending`, `working`, `completed`, `cancelled`)
* Customers can only see their own (CID) records
* When Customers create RVS records, they only need to enter their name. When Service staff review and assign RVS records, they need to resolve the name to an existing CID+VIN combination.
* Creating a new RVS requires: RID, VIN, Customer Name. SID, Status, and DateCreated are supplied by server.
* Marking a record `completed` requires RID, CID, VIN, SID, WID, Customer Name, Requested Work, DateCreated, DateUpdated, and Status (`completed`)

