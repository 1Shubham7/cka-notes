### Metrics Server

Metrics Server is deployed as Deployment and it provides resource usage metrics (like CPU and memory) for the nodes and pods.

you can use `kubectl top pods` or `kubectl top nodes` for that.

it is tought to find docs for it so simply search "metrics server installation", click on the first discussion link. you will find this command:

`kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml` (even this may not work) 

## Requests and Limits:

**Requests:** The minimum amount of a resource (CPU or memory) given to the pod.
**Limits:** The maximum amount of a resource (CPU or memory) that a container can use.

e.g.:

```
apiVersion: v1
kind: Pod
metadata:
  name: memory-demo-2
  namespace: mem-example // also see this, we can specify the namespace in the metadata as well :)
spec:
  containers:
  - name: memory-demo-2-ctr
    image: polinux/stress
    resources:
      requests:
        memory: "50Mi"
      limits:
        memory: "100Mi"
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "250M", "--vm-hang", "1"]
```
