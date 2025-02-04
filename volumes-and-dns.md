You can create a volume and pod in same file also. here it is emptyDir so volume only persistant till pod in not killed: (also see that volumeMount is inside container because mounting will be done inside container 
but volume should be outside container.)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: redis-pod
spec:
  containers:
  - image: redis
    name: redis
    volumeMounts:
    - name: redis-storage
      mountPath: /data/redis
  volumes:
  - name: redis-storage
    emptyDir: {}
```

Otherwise this will not be deleted with pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pv-recycler
spec:
  restartPolicy: Never
  volumes:
  - name: vol
    hostPath:
      path: /any/path/it/will/be/replaced
  containers:
  - name: pv-recycler
    image: "registry.k8s.io/busybox"
    command: ["/bin/sh", "-c", "test -e /scrub && rm -rf /scrub/..?* /scrub/.[!.]* /scrub/*  && test -z \"$(ls -A /scrub)\" || exit 1"]
    volumeMounts:
    - name: vol
      mountPath: /scrub
```

- how will you add text to a file without vim : `echo "asdfasdf" > a.txt`

- how to check the processes running: `apt-get update && apt-get install procps -y` and then do `ps aux`. a means all users, u means user fiendly output, x means show process not attached to terminal.

- to kill a process just do `kill [PROCESS ID]`. if you want to force kill: `kill -9 [PROCESS ID]`

![image](https://github.com/user-attachments/assets/491e63b0-9526-4a2d-957b-7c6f2a829c5a)


## CoreDNS

If you have two pods and two services and we try doing `k exec -it nginx -- curl nginx2` it should work. but if this gives error and this command - `k exec -it nginx -- curl [IP]` works fine, that means there is some issue with your coreDNS, you check if the pods of coreDNS are 0, if yes, scale the deployment.

- So coreDNS is present as a deployment in the cluster and it also need a service called kube-dns.
- imp files inside pod for coredns are `etc/resolv.conf` and `etc/hosts` (know about them in whatsapp video).
- Also coreDNS might fail if you don't have a CNI.
- if this comes in cka, then first search "Debugging DNS Resolution" in kubernetes docs, that will help.
