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

