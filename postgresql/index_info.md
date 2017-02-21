# show index info for a table

```sql

select
    t.relname as table_name,
    i.relname as index_name,
    a.attname as column_name,
    pg_size_pretty(pg_relation_size(quote_ident(i.relname)::text)) AS index_size
from
    pg_class t,
    pg_class i,
    pg_index ix,
    pg_attribute a
where
    t.oid = ix.indrelid
    and i.oid = ix.indexrelid
    and a.attrelid = t.oid
    and a.attnum = ANY(ix.indkey)
    and t.relkind = 'r'
    and t.relname = 'trainings'
order by
    t.relname,
    i.relname;
```
