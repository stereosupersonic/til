# fetch all uniq values from a column

```
Location.order(:country).distinct.pluck(:country)
```
