# Serialize to PORO

can be used for the refactoring: replace primitive with object

[serialize](https://api.rubyonrails.org/classes/ActiveRecord/AttributeMethods/Serialization/ClassMethods.html)

## Example

```
class User
  # role is a string field
  serialize :role, Role
end


class Role
  
  attr_readr :name

  def initialize(role_name)
    @name = role_name
  end  

  def self.load(value)
     Role.new value
  end

  def self.dump(value)
    Role.new(value).name
  end

```
