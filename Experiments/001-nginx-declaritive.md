
## Expeirment 1 - simple nginx pod declaritive method
File: pod.yaml
```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

Create Pod with the help of pod.yaml - declarative method
```bash
kubectl apply -f pod.yaml
```

Check the running status of pod

```bash
kubectl get pods
```

When using killercoda. Port forwarding, extra --address flag is used [ https://killercoda.com/playgrounds/scenario/kubernetes]
```bash
kubectl port-forward --address 0.0.0.0 pod/nginx-pod 3333:80
```

Port forwarding in localhost / local system
```bash
kubectl port-forward pod/nginx-pod 3333:80
```
