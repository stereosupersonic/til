# Use attributes with types on active model (auto. cast params)

```
class SalesReport
  include ActiveModel::Model
  include ActiveModel::Attributes

  attribute :start_date, :date
  attribute :end_date, :date
  attribute :min_items, :integer

  def run!
    # Do some cool stuff
  end
end

report = SalesReport.new(start_date: "2020-01-01", end_date: "2020-03-01", min_items: "10")

# Now the attributes are native types!

report.start_date
# => Wed, 01 Jan 2020
report.min_items
# => 10

```
