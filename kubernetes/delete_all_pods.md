# Delete all Pods

```
for pod in $(kubectl get pods -o name  --namespace=bodyweight-api --context=prod)
do
  kubectl delete $pod --namespace=bodyweight-api --context=prod; sleep 6;
done

```
