# Add an index on postgresql

By default, Postgres locks writes (but not reads) to a table while creating an index on it.
That can result in unacceptable downtime during a production deploy.
On a large table, indexing can take hours.

```
class AddIndexToAsksActive < ActiveRecord::Migration
  disable_ddl_transaction!

  def change
    add_index :asks, :active, algorithm: :concurrently
  end
end
```

found it here: https://robots.thoughtbot.com/how-to-create-postgres-indexes-concurrently-in

PR comment: https://github.com/freeletics/fl-backend-rails/pull/421#discussion_r41237874
Postgres Doc on concurrently: http://www.postgresql.org/docs/9.4/static/sql-createindex.html#SQL-CREATEINDEX-CONCURRENTLY
