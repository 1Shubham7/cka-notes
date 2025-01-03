Taints and tolerations are used to control how pods are scheduled on nodes.  

Taints are added to nodes to repel pods unless those pods are explicitly allowed.
Tolerations are added to pods to indicate that they can tolerate the taints of the nodes.

Taint = key=value:Effect

Effects:

1. ***NoSchedule:*** don't add pods that do not tolerate the taint.
2. ***PreferNoSchedule:*** no strict enforcement, but don't add pods that do not tolerate the taint.
3. ***NoExecute:*** don't add pods that do not tolerate the taint as well as remove existing pods without tolerations.

To add taints:

`kubectl taint node worker gpu=true:NoSchedule`

To remove taint, just add '-':

`kubectl taint node worker gpu=true:NoSchedule-`

Adding taints to pods, you can simply search that in k8s docs:

```yamlapiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoSchedule"
status: {}
```
