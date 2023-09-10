# TwoContainerPod
# POD with TWO Container Demo
Create nginx-curl-pod.yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx-curl
  labels:
    app: nginx-curl
spec:
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
  - name: sidecar 
    image: curlimages/curl
    command: ["/bin/sh"]
    args: ["-c", "echo Hello from the sidecar container; sleep 300"] 
---
*APPLY POD***
```bash
kubectl apply -f <pod name>.yaml
kubectl apply -f nginx-curl-pod.yaml
kubectl get pod
```
*CHECK CONNECTION inside POD***
```bash
kubectl exec -it <pod name> -c <container name> -- <command>
kubectl exec -it nginx-curl -c sidecar -- /bin/sh
```open shell in sidecar container
netstat -ln
```check listening ports sidecar container
curl localhost:80
```

