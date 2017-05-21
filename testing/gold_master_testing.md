# Gold Master test

testing a defined subset of prodcution data with an expected result like a html web site

## Rails conf 2017
Observing Chance: A Gold Master Test in Practice by Jake Worth https://www.youtube.com/watch?v=D9awDBUQvr4

 https://github.com/hashrocket/hr-til/blob/gold-master-demo/spec/features/gold_master_spec.rb

```ruby

require 'rails_helper'

describe 'gold master spec' do

  before do
    ActiveRecord::Base.connection.execute <<-SQL
      truncate schema_migrations;
      #{Rails.root.join('spec/fixtures/gold_master.sql').read}
    SQL

    visit root_path
  end

  specify 'the homepage does not change' do
    page_html = page.html
    gold_master_file = Rails.root.join('spec/fixtures/gold_master.txt')

    if !gold_master_file.exist?
      gold_master_file.write(page_html)
    else
      gold_master = gold_master_file.read

      if gold_master != page_html
        gold_master_file.write(page_html)
      end

      expect(page_html).to eq(gold_master)
    end
  end
end


```
