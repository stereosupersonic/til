# Joins in rails

[SQL Joins](../sql/joins.md)


## inner join

**includes**
```
User.joins(:notification_info).where(notification_infos: {optivo_blacklisted: [false, nil], optivo_bounced: [false, nil]})
```
becomes

```
SELECT "users".* FROM "users" INNER JOIN "notification_infos" ON "notification_infos"."user_id" = "users"."id" WHERE ("notification_infos"."optivo_blacklisted" = 'f' OR "notification_infos"."optivo_blacklisted" IS NULL) AND ("notification_infos"."optivo_bounced" = 'f' OR "notification_infos"."optivo_bounced" IS NULL)
```

## outer join

**includes**
```
User.includes(:notification_info).where(notification_infos: {optivo_blacklisted: [false, nil], optivo_bounced: [false, nil]})
```

becomes

```
SELECT ... FROM "users" LEFT OUTER JOIN "notification_infos" ON "notification_infos"."user_id" = "users"."id" WHERE ("notification_infos"."optivo_blacklisted" = 'f' OR "notification_infos"."optivo_blacklisted" IS NULL) AND ("notification_infos"."optivo_bounced" = 'f' OR "notification_infos"."optivo_bounced" IS NULL)
```
