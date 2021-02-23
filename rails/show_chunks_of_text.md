# Show relevant chunks of text

## excerpt

https://edgeapi.rubyonrails.org/classes/ActionView/Helpers/TextHelper.html#method-i-excerpt

```
@product.description = "A one-of-a-kind vintange DHH coffee mug signed by the man himself!"

excerpt(@product.description, "coffee", radius: 10)
=> "...tange DHH coffee mug signe..."
```


## truncate

https://edgeapi.rubyonrails.org/classes/ActionView/Helpers/TextHelper.html#method-i-truncate

```
truncate("Once upon a time in a world far far away")
# => "Once upon a time in a world..."

```
