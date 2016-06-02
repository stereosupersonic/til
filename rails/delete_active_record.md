# delete vs. destroy

Basically destroy runs any callbacks on the model  while delete doesn't.

## ActiveRecord::Persistance.delete
### delete will only delete current object record from db but not its associated children records from db.
```
Deletes the record in the database and freezes this instance to reflect that no changes should be made (since they can't be persisted). Returns the frozen instance.

The row is simply removed with an SQL DELETE statement on the record's primary key, and no callbacks are executed.

To enforce the object's before_destroy and after_destroy callbacks or any :dependent association options, use #destroy.
```

## ActiveRecord::Persistance.destroy
## #destroy will delete current object record from db and also its associated children record from db.
```
Deletes the record in the database and freezes this instance to reflect that no changes should be made (since they can't be persisted).

There's a series of callbacks associated with destroy. If the before_destroy callback return false the action is cancelled and destroy returns false. See ActiveRecord::Callbacks for further details.
```
