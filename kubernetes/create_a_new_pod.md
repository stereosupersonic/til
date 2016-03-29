# Create a new pod


create a yaml file like bodyweight-api.yml

```
kind: Pod
apiVersion: v1
metadata:
 name: my-name
 namespace: bodyweight-api
spec:
  containers:
  - name: rails
    image: "docker.freeletics.com/bodyweight-rails:2016-03-21_08-39" # Docker container
    imagePullPolicy: IfNotPresent
    ports:
    - name: http
      containerPort: 9080
      protocol: TCP
    command:
    - tini
    - sleep
    - infinity
    env:
    - name: ROLE
      value: api
    - name: RAILS_ENV
      value: production
    - name: POD_NAMESPACE
      valueFrom:
        fieldRef:
          fieldPath: metadata.namespace
    volumeMounts:
    - name: rails-secrets
      mountPath: /run/secrets/freeletics.com/rails
      readOnly: true
  volumes:
  - name: rails-secrets
    secret:
      secretName: rails
  imagePullSecrets:
  - name: docker-registry
```

Create pod
```
kubectl create -f bodyweight-api.yaml
```

you should have a running pod named *my-name*
