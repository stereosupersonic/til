# Upload a file to a Pod

```
cat <source_file> | kubectl exec -i <pod> -- bash -c 'cat >> <target_file>'

```
