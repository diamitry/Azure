Azure Data Factory is a powerful ETL tool that with the release of the Dataverse connector can move data into your Dataverse environment in bulk and with ease.
However, the challenge comes when moving data into the polymorphic lookups (account, contact, owner, team, etc.). The documentation is not very clear on how exactly to joggle between the GUIDs, entity names, shortcuts, and etc.
Here's what you can do:
- For polymorphic lookup columns, when mapping them in the data flow step, in addition to the Guid colum, pass on a virtual column name that will contain a single value for every row being inserted, such as account, contact, systemuser, etc. The sample row in the data preview should look like Guid, then a value "account" for every single row being inserted.
- For polymorphic lookup columns, when mapping them in the copy activity, map the UTF8 to the guid (i.e. accountid to accountid), and map the row value (i.e. account) to the object@EntityReference virtual column (i.e. account@entityreference)
- Make sure the fields maps exactly to the schema names in the dataverse, and respect the case
- It is highly unlikely your copy activity will contain just a single entity, so the "shortcut" method with {lookup_field_name}@EntityReference might not be a best approach
