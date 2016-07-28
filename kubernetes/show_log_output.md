# show logs from a pod

[docs](http://kubernetes.io/docs/user-guide/kubectl/kubectl_logs/)

```
  kubectl --namespace=<name> logs <pod> -f <container>
```

Example:
```
  kubectl --namespace=bodyweight-api logs api-1779665279-wzvoj -f rails
```
