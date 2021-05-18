# Configurable

https://api.rubyonrails.org/classes/ActiveSupport/Configurable.html

 which adds a config method to the class which can store some configuration.

```
class Example
  include ActiveSupport::Configurable
end

Example.configure do |config|
  config.some_option = 'value'
end
# or
Example.config.some_option = 'value'

# fetch option
Example.config.some_option #=> "value"


```
