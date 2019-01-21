# Remove leading or trailing whitespace

```sql
 update negotiations 
 set override_recipient_address = TRIM(override_recipient_address) 
 WHERE CHAR_LENGTH(override_recipient_address) != CHAR_LENGTH(TRIM(override_recipient_address))
```
