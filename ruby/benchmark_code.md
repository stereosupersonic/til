# Benchmark ruby code

## simple
```
Benchmark.bm(10) do |x|
  x.report('f1:')         { function1 }
  x.report('f2:')  { function2 }
end

```

## better with benchmark/ips
```
gem "benchmark-ips"

require 'benchmark/ips'
user_ids = (1..5000).to_a

Benchmark.ips do |x|
  x.report("array: ")  { User.select(:id).where(emails_allowed: true).where("id != all(array[?])", user_ids).find_each {} }
  x.report("not in: ") { User.select(:id).where(emails_allowed: true).where.not(id: user_ids).find_each {} }

  x.compare!
end

```
