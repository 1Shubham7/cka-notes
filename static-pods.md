***Manual Scheduling:*** using `nodeName: cka-cluster-3-worker` we do not need the scheduler to schdule our pods, we define the node on our own:

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: pod
  name: nginx
spec:
  containers:
  - image: nginx
    name: pod
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  nodeName: cka-cluster-3-worker
status: {}
```

All the control plane components like scheduler, api-server etc. are actually manifests present in `etc/kubernetes/manifests/` of our control plane, now locally this control plane 
is a docker container so we do:
`docker exec -it cka-cluster-3-control-plane bash` to get into control plane and then `etc/kubernetes/manifests/` but for cka, you will have to do ssh into the control plane which will be a 
virtual machine. to troubleshoot any issue with the control plane components go there.
