# Replace Timecop With Rails Time Helpers in RSpec

https://andycroll.com/ruby/replace-timecop-with-rails-time-helpers-in-rspec/

```
RSpec.configure do |config|
  config.include ActiveSupport::Testing::TimeHelpers
end

travel_to Time.zone.local(2004, 11, 24, 01, 04, 44) do
 # do something in the past
end

```
https://api.rubyonrails.org/v5.2.2/classes/ActiveSupport/Testing/TimeHelpers.html

