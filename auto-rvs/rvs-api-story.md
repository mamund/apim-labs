# Request for Vehicle Service (RVS)

## Purpose
We use the Request for Vehicle Service (RVS) process to manage customer requests for maintainence of thier vehicle.

## Actions
There are two personas for the RVS process:
* Customers
* Service Staff

### Customers can do the following:
* Create a new RVS
* Update and exsiting RVS (as long as it is not in progress)
* Cancel an existing  RVS (as long as it is not in progress)
* List previous RVS documents (including filtering by date, vehicle ID, and status)

### Service Staff can:
* Update an existing RVS
* Assign CID to an existing RVS
* Assign SSID (Service Staff identifier) to an existing RVS
* Change the status of an existing RVS (pending, working, completed, cancelled)
* Attach an existing Service Work Record (SWR) to an existing RVS (see below)

## Data
And RVS record consists of the following:
* RID (RVS identifier)
* CID (Customer identifier)
* VIN (Vehicle identification number)
* SSID (Service Staff identifier)
* SID (Service Work Record)
* Customer Name (open text, resolved against CID)
* Requested Work (open text, multi-line)
* Status (`pending`, `working`, `completed`, `cancelled`) defaults to pending
* DateCreated
* DateUpdated

### Notes
* RID is generated when the record is created
* CID is added after the customer creates the record. Initially, customer only adds their name.
* VIN is standardized data point (NHTSA, 1954)
* SSID is a pointer to an existing Service Staff record (see below)
* SID is a pointer to an existing Service Work Record created by Service staff (see below)
* Customer Name is open-text field filled in by customer, updated by Service Staff
* Requested work is open-text, multi-line field filled in by customer
* Status is set to `pending` when RVS is created. It is modified by Service staff (`working`, `completed`, `cancelled`). Customers can mark a `pending` record as `cancelled`.
* DateCreated is the UTC date/time the RVS was first created
* DateUpdated is the UTC date/time the RVS as modifed in any way

### Service Staff Record (SSR)
This is a separate process covered elsewhere in this documentaiton.

### Service Work Record
This is a separate process covered elsewhere in this documentation. 

## Work
* Listing RVS records should support paging (`first`, `previous`, `next`, `last`).
* Filtering the list of RVS records support support:
  * DateCreated (UTC)
  * VIN (portion)
  * CID (portion) - Service Staff only
  * Status (`pending`, `working`, `completed`, `cancelled`)
* Customers can only see their own (CID) records
* When Customers create RVS records, they only need to enter their name. When Service staff review and assign RVS records, they need to resolve the name to an existing CID+VIN combination.
* Creating a new RVS requires: RID, VIN, Customer Name. SID, Status, and DateCreated are supplied by server.
* Marking a record `completed` requires RID, CID, VIN, SSID, SID, Customer Name, Requested Work, DateCreated, DateUpdated, and Status (`completed`)

