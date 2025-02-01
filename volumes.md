You can create a volume and pod in same file, but emptyDir is only persistant till pod in not killed: (also see that volumeMount is inside container because mounting will be done inside container 
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
