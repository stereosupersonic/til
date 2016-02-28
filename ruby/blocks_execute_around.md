# Blocks execute around

## Example Logging
```
def with_logging(description)
  begin
    @logger.debug("Start #{description}")  
    yield
    @logger.debug("Completed #{description}")  
  rescue
    @logger.error("#{description} failed!")  
    raise
  end
end

# use it
with_logging("compute something") do
  25 * 26
end
```

### In the wild:
* [say_with_time](https://github.com/rails/rails/blob/v4.2.2/activerecord/lib/active_record/migration.rb#L629)
* [with return value](https://github.com/rails/rails/blob/v4.2.2/activerecord/lib/active_record/transactions.rb#L347)

## Example Intitalization Block
```
class Document
  attr_accessor :title, :number
  def initialize
    yield( self ) if block_given?
  end
end

# use it
Document.new do |doc|
  doc.title  = "something"
  doc.number = 123
end
```
