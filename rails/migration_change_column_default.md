# Change the default value of a column

http://apidock.com/rails/ActiveRecord/ConnectionAdapters/SchemaStatements/change_column_default

```
class ChangeUsers < ActiveRecord::Migration
  def up
    change_column_default :users, :measurement_system, 1
  end

  def down
    change_column_default :users, :measurement_system, nil
  end
end
```

Article: http://engineering.wework.com/data/2015/11/05/add-columns-with-default-values-to-large-tables-in-rails-postgres/
