# memoization pitfall
### if method can return false or nil, and you want to memoize it, use defined?(@result) instead of ||=

## Example Logging
```
# bad
def flagged?
  @flagged ||= fetch_value_from_server # it fetches always when  @flagged  = false or nil
end

# better
def flagged?
  return @flagged if defined?(@flagged)
  @flagged = fetch_value_from_server
end
```

http://www.jetthoughts.com/blog/tech/2015/08/17/how-to-memoize-false-and-nil-values.html
