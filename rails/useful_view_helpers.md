# Useful view helpers

```
def unknown(attribute)
  attribute.presence || "&nbsp;".html_safe
end

alias_method :u, :unknown
```


```
<dd class="col-lg-6"><%=u object.method_that_could_return_nil %> </dd>
```
