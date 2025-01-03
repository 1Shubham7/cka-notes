# cka-notes

![340174607-b1bfe6ae-a1e6-4b04-8486-272d3ed380bc](https://github.com/user-attachments/assets/fa9c49d6-181f-48ad-ba2b-031f605feb82)

### Docker Multi-stage builds tips 

- Use Official Base Images: Start with minimal base images like alpine or distroless when possible.
- Separate build-time and runtime dependencies to keep the final image lightweight.
- Use .dockerignore to exclude files and directories not needed in the build context.
- Order Instructions Strategically: Place less frequently changing commands first to leverage layer caching effectively.
- Use && or multi-line scripts in a single RUN instruction to reduce the number of layers.
- Remove package cache files and unnecessary dependencies after installation (e.g., apt-get clean or rm -rf /var/lib/apt/lists/*).
- Install only the libraries and tools needed for the application to run.
- Avoid installing unnecessary debugging tools in production images.

### Creating multi node cluster with kind:

we can use this command to create cluster with kind:

but it is a single node cluster with worker and control plan in same node, for multi node cluster, go to kind docs and search "multi":

```yml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

------------------------------------------

**You will get access to kubernetes.io/docs and /blogs for CKA**

- To get the apiVersion, `kubectl explain pod`
- IMP: to get the yaml file:
  `kubectl run nginx --image=nginx --dry-run=client -o yaml > pod.yaml`

  // for pod we can use "run" only, but for deployment we can use "run" or "create":

  `kubectl run pod --image=nginx --dry-run=client -o yaml > pod.yaml`
  
  `kubectl run deployment nginx-depl --image=nginx --dry-run=client -o yaml > depl.yaml`
  
  `kubectl create deployment nginx-depl --image=nginx --dry-run=client -o yaml`

  This is the best 

***--dry-run=client*** is the keyword here, don't forget that

## For troubleshooting:

1. you can get details about k8s objects using - `kubectl describe pod [NAME]`
2. you can bacially edit the k8s objects using -  `kubectl edit pod [NAME]`

## Scaling ReplicaSets:

1. rewrite the yaml file
2. edit using `kubectl edit`
3. imperetive way - `kubectl scale --replicas=10 rs/nginx-rs`

## Getting inside pods and containers:

- to get inside a pod:
`kubectl exec -it multi-container-pod -- sh`

- to get inside a specific pod of a container use -c:
`kubectl exec -it multi-container-pod -c my-app -- sh`

- To prite environment variables of a pod: after the -- there is a command, so it could also be a command like printenv"
`kubectl exec -it multi-container-pod -- printenv`

### if you don't remember anything, use --help

e.g. : `kubectl scale --help`

### Change image in deployment

`kubectl set image deploy [DEPLOYMENT NAME] [CONTAINER NAME]=[NEW IMAGE]`
`kubectl set image deploy nginx-depl nginx-container=nginx:1.9.1`

Then you can also check out rollout history:
`kubectl rollout history deploy [NAME]`

Then you can also roll back this:
` kubectl rollout undo deploy [NAME]`

## Setting Alias

1.  `vim .bash_profile`
2.  then in the file add `alias 'k=kubectl'`
3.  `source .bash_profile`

Also in exam, for alias and autocompleting tags, just go to cheetsheet and the first topic is that only.

for setting alias in exam just use `alias 'k=kubectl'` in shell. also you can't set alias like `alias g='get'`, only stuff like `alias kg=kubectl get`

## Tips:

1. Metadata.Name should not have capital letters, so loadBalancer -> load-balancer

## Miscellenaous 

- Assign the change cause "Pick up patch version" to the revision.

`kubectl annotate deployment <deployment-name> kubernetes.io/change-cause="Pick up patch version"`

- Create service in declarative way:
 
`kubectl expose deploy [DEPLOYMENT_NAME] --port=80 --target-port=8000` (find this on the cheatsheet if you face difficulties)

- `-A` is for all namespaces:
`kubectl get pods -A` will give pods of all ns.

- use `| grep` for searching:

`kubectl get pods | grep my-app` will give all pods that has my-app in it. 

- use `--selector` to filter by labels:

`kubectl get pods --selector env=demo`

## Imp Questions

1. for python app we need a python runtime, but for go app we dont need a go runtime why?
2. Why multi stage builds?
3. what are distroless images

## Tasks before the exam:

1. ***Make sure to watch day 10 video 20:00 onwards to know about fully qualified domain name***







## Assignments:

- [x] Day 14
