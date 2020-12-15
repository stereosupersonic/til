## Testing

### rspec

```
#in Gemfile group :development, :test add 
gem "rspec-rails"
#in command line
bundle install
rails generate rspec:install
```

### factory 

https://github.com/thoughtbot/factory_bot_rails
```
#in Gemfile group :development, :test add 
 gem "factory_bot_rails"
```

### capybara 
https://github.com/teamcapybara/capybara

```
#in Gemfile group :test add 
  gem "capybara"
  gem "launchy" # for capybara save_and_open_page
  gem "webdrivers"
```

### new file spec/capybara_helper.rb

```
touch spec/capybara_helper.rb
```

```
# frozen_string_literal: true

require "rails_helper"
require "capybara/rspec"

RSpec.configure do |config|
  config.include Capybara::RSpecMatchers

  Capybara.default_max_wait_time = 10 # The maximum number of seconds to wait for asynchronous processes to finish.
  Capybara.default_normalize_ws = true # match DOM Elements with text spanning over multiple line

  config.before(:each, type: :system) do
    driven_by :rack_test
  end

  config.before(:each, type: :system, js: true) do
    # https://api.rubyonrails.org/v6.0.1/classes/ActionDispatch/SystemTestCase.html#method-c-driven_by
    browser = ENV["SELENIUM_BROWSER"].presence&.to_sym || :headless_chrome
    driven_by :selenium, using: browser, screen_size: [1600, 1400]
  end
end

```

### setup system spec for root page

```
mkdir -p spec/system/
touch spec/system/welcome_spec.rb
```

#### add first test

```
require "capybara_helper"

describe "welcome", type: :system do
  it "shows the tranding tracks of this year" do
    visit "/"

    expect(page).to_not have_content("Welcome")
  end
end
```
