# Keyword Arguments with options

```ruby
def foo(a:, **b)
  [a, b]
end

foo(a: 1, b: 2, c:3) #=> [1, {:a=>2, :b=>3}]
```

[Article](http://brainspec.com/blog/2012/10/08/keyword-arguments-ruby-2-0/)
