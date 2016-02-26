# Use max_by over sort_by.last

http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-max_by

```
a = %w(albatross dog horse)

# before
a.sort_by(&:size).last

# after
a.max_by(&:size)
```
