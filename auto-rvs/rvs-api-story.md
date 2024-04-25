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
* Change the status of an existing RVS (pending, working, completed, cancelled)
* Attach an existing Service Work Record (SWR) to an existing RVS (see below)

## Data
And RVS record consists of the following:
* RID (RVS identifier)
* CID (Customer identifier)
* VIN (Vehicle identification number)
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
* SID is a pointer to an existing Service Work Record created by Service staff (see below)
* Customer Name is open-text field filled in by customer, updated by Service Staff
* Requested work is open-text, multi-line field filled in by customer
* Status is set to `pending` when RVS is created. It is modified by Service staff (`working`, `completed`, `cancelled`). Customers can mark a `pending` record as `cancelled`.
* DateCreated is the UTC date/time the RVS was first created
* DateUpdated is the UTC date/time the RVS as modifed in any way

### Service Work Record
This is a separate process covered elsewhere in this documentation. 

## Work
TK

