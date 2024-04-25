# Request for Vehicle Service Vocabulary

## Actions
* CreateRVS
* UpdateRVS
* CancelRVS
* AssignServiceStaff
* AssignServiceRecord
* AssignCustomer
* MarkRVSWorking
* MarkRVSCompleted
* ListRVS
* FilterRVS

## Properties
* RID [UUID]
* CID [UUID]
* VIN [NHTSA, 1954]
* SID [UUID] [array] 
* SSID [UUID] [array]
* Status (`pending`, `working`, `completed`, `cancelled`)
* CustomerName [text]
* RequestedWork [multi-line text]
* ServiceNotes [multi-line text]
* DateCreated [UTC date/time]
* DateUpdated [UTC date/time]


