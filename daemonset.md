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

```sh
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday)
# │ │ │ │ │                                   OR sun, mon, tue, wed, thu, fri, sat
# │ │ │ │ │ 
# │ │ │ │ │
# * * * * *
```

you can find all this on docs

![image](https://github.com/user-attachments/assets/55012d47-979c-46f7-b575-8cee56bb8c22)

![image](https://github.com/user-attachments/assets/80bfeb5f-07b2-4632-ab28-e39bf382b4ab)
