# Hash with default values

https://www.rubytapas.com/2012/12/05/episode-032-hash-default-blocks/

```
word_count = {}
text = <<END
I'm your only friend
I'm not your only friend
But I'm a little glowing friend
But really I'm not actually your friend
But I am
END

# before
text.split.map(&:downcase).each do |word|
  word_count[word] ||= 0
  word_count[word] += 1
end

# after
word_count = Hash.new do |hash, missing_key|
  hash[missing_key] = 0
end

text.split.map(&:downcase).each do |word|
  word_count[word] += 1
end
```

## with default_proc
```
config = Hash.new do |h,k|
  h[k] = Hash.new(&h.default_proc)
end

config[:production][:database][:adapter] = 'mysql'
config[:production][:database][:adapter] # => "mysql"

```
