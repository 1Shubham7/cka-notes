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

#### Selectors

With taints and tolerations, nodes were deciding which pod to choose, with `nodeSelector` the pods decide which node to choose:

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx-two
  name: nginx-two
spec:
  containers:
  - image: nginx
    name: nginx-two
    resources: {}
  dnsPolicy: ClusterFirst
  nodeSelector:
    gpu: "false"
  restartPolicy: Always
status: {}
```

to add labels to nodes or even pods :

`kubectl label node cka-cluster-3-worker gpu=false`

For these yaml go to docs and find them at the last moment and cram that journey or carm these systaxes itself if you can't find docs, if you forget, check docs because you may get confused about nodeSelector or Taints syntax which is confusing. But for nodeSelec
