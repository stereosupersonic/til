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
  gem "selenium-webdriver"
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

  Capybara.default_max_wait_time = 10
  Capybara.default_normalize_ws = true # match DOM Elements with text spanning over multiple line

  if ENV["USE_SELENIUM"].present?
    Capybara.register_driver :selenium do |app|
      Capybara::Selenium::Driver.new(app, browser: (ENV["SELENIUM_BROWSER"].presence || :chrome).to_sym)
    end

    Capybara.register_driver :headless_chrome do |app|
      capabilities = Selenium::WebDriver::Remote::Capabilities.chrome(
        chromeOptions: { args: %w[no-sandbox headless disable-gpu window-size=1366,1768] }
      )
      Capybara::Selenium::Driver.new(app,
                                     browser:              (ENV["SELENIUM_BROWSER"].presence || :chrome).to_sym,
                                     desired_capabilities: capabilities)
    end

    Capybara.javascript_driver = :selenium
  else
    config.before(:each, type: :system) do
      driven_by :rack_test
    end

    config.before(:each, type: :system, js: true) do
      driven_by :selenium_chrome_headless
    end
  end
end

```