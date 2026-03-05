1. Issue: Data is overlapping on start and end due to aggresgating sessions, making things look to long 
Solution: Split sessions, also add logic in upstream (python) to prevent sessions longer than 9 seocnds to register 

2. Browser data not syncing at all
Solution: It was an issue with the .bat file for running the python script in task scheduler 

3. Auth can only be scoped by user, not application
Dev tier limitation: Used bearer token and save secrets in lambda only, NOT in chrome extension

4. Domains are not updating on action type, because it is linked to the backing dataset 
Solution: Reference the ontology, not the backing dataset

5. Workshop unable to reference linked object in filter
Solution: I had the order wrong in creating universal filter, the correct way was filter by child then link to get parent object fields

6. How would I get insight from the dashboard? 
Solution: Created AIP logic flow
