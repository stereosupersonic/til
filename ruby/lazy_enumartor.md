# lazy enumerator

run a expensive iteration until its fullfilled 

like you search for the first element that is present, for that you don't need to iteratate over all entries

example:

```
  def self.env_or_constant(name)
    [
     proc { ENV[name].presence },
     proc { Object.const_defined?(name).presence && const_get(name) },
     proc { yield if block_given? }
   ].lazy.map(&:call).detect { |e| !e.nil? }
  end
```

### This code will "hang" and you'll have to ctrl-c to exit

```
(1..Float::INFINITY).reject { |i| i.odd? }.map { |i| i*i }.first(5)

```

#### this will work

```
(1..Float::INFINITY).lazy.reject { |i| i.odd? }.map { |i| i*i }.first(5) #=> [4, 16, 36, 64, 100]

```
