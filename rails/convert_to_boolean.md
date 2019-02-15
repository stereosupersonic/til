# Convert to boolean 

```ruby
  
  ActiveRecord::Type::Boolean.new.cast("true") #=> true

  ActiveRecord::Type::Boolean.new.cast("false") #=> false

  ActiveRecord::Type::Boolean.new.cast(nil) #=> false
  
  ActiveRecord::Type::Boolean.new.cast(1)  #=> true
  ActiveRecord::Type::Boolean.new.cast(0)  #=> false
  ActiveRecord::Type::Boolean.new.cast(2)  #=> true

  ActiveRecord::Type::Boolean.new.cast(true) #=> true
```

https://github.com/rails/rails/blob/94b5cd3a20edadd6f6b8cf0bdf1a4d4919df86cb/activemodel/lib/active_model/type/boolean.rb#L29