# Download a file from a Pod

```
kubectl exec <pod> cat /path/to/remote/file > /path/to/local/file`
```

In the wild

```
kubectl exec michael-pw-reset --namespace=bodyweight-api --context=prod cat /app/user_list.csv > /Users/michaeldeimel/entwicklung/freeletics/user_list.csv
```
