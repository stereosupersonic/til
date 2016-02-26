# Use Rails.root.join

http://apidock.com/rails/Rails/root/class

```
# BEFORE
File.join(Rails.root, "spec/fixtures/unsubscribers_15022016_.csv")

# AFTER
Rails.root.join("spec/fixtures/unsubscribers_15022016_.csv")
```
