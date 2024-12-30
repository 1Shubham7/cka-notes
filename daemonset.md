## DaemonSet

DaemonSet is a Kubernetes object that create 1 replica of a pod in all the nodes of cluster. used for deploying apps for monitoring, logging, etc.

Example: Kube-Proxy is deployed as a DaemonSet, and other CNI plugins that we will discuss later, like Weave-net etc.

Same as deployment, just don't specify replicas and change kind:

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: my-daemon-set
spec:
  template:
    metadata:
      labels:
        env: demo
    spec:
      containers:
      - image: nginx
        name: nginx
        ports:
        - containerPort: 80
  selector:
    matchLabels:
      env: demo
```

## Jobs and CronJobs

A Job is a Kubernetes resource that runs a set of tasks (pods) to completion (just once). and CronJob creates Jobs periodically, or you can say that it runs a set of tasks perdiocially like every month etc.

ConJobs are used for generating weekly reports, for cleaning up logs, etc. Jobs are used for installation scripts etc. 
