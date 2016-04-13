# Make a class abstract

http://api.rubyonrails.org/classes/ActiveRecord/Inheritance/ClassMethods.html#method-i-abstract_class-3F

```
class MySuperClass < ActiveRecord::Base
  self.abstract_class = true
end

class MyChild < MySuperClass
end

MySuperClass.new # => NotImplementedError: MySuperClass is an abstract class and cannot be instantiated.

```
