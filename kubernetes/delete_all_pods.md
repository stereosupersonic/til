# Delete all Pods

```
for pod in $(kubectl get pods -o name  --namespace=bodyweight-api --context=prod | sed -e 's/^pod\///')
do
  kubectl delete pod $pod --namespace=bodyweight-api --context=prod; sleep 6;
done

```
