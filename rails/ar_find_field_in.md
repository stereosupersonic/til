# Find with in

```ruby
  where(ignore_performance: [nil, false])  
```

is

```sql
SELECT "trainings".* FROM "trainings" WHERE ("trainings"."ignore_performance" = 'f' OR "trainings"."ignore_performance" IS NULL)
```
