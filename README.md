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

  // for pod we don't say pod but for deployment we also say deployment:
  `kubectl run deployment nginx-depl --image=nginx --dry-run=client -o yaml > depl.yaml`
  OR create gives better than run:

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

## Miscellenaous 

- Assign the change cause "Pick up patch version" to the revision.

`kubectl annotate deployment <deployment-name> kubernetes.io/change-cause="Pick up patch version"`

## Imp Questions

1. for python app we need a python runtime, but for go app we dont need a go runtime why?
2. Why multi stage builds?
3. what are distroless images
