### HELM

To install helm: `sudo snap install helm --classic`

- When a helm chart is applied, a single release of the app is installed to the cluster (helm charts are nothing but `.yaml` files). and we can use `values.yaml` file to customize the helm charts. `Chart.yaml` has info about the charts. if apiversion in chart.yaml is v1 or not specified then it is helm 2. If it is v2, then it is helm3.

- to add the repo: `helm repo add [NAME] [LINK]`
- to install chart: `helm install [RELEASE-NAME] [CHART]`
- to upgrade release: `helm upgrade [RELEASE-NAME] [CHART]`
- to delete: `helm uninstall [RELEASE-NAME]`
- to list releases : `helm list` (Releases are nothing but apps, not calling them apps because we can install multiple releases of a single helm chart or application.
- Use `--set abc="xyz"` or `--values v.yaml` to change the values while `helm install`. OR:
- do `helm pull --untar [CHART]` and changes to the values.yaml and then install: `helm install [RELEASE-NAME] [DIR_PATH]`
-  `helm search [hub or repo] [CHART_NAME] ` to search for charts
-  `helm history [RELEASE_NAME]` to check the histroy of the release
-  `helm rollback [RELEASE_NAME] [REVISION_NO]` to rollback, revision no. you can find through helm histroy.

![image](https://github.com/user-attachments/assets/65810fa2-61c4-47b6-b5a8-6576f0bac018)

![image](https://github.com/user-attachments/assets/7a4f91c9-c6b9-4261-8168-93fc005ef3cb)


## Kustomize

![image](https://github.com/user-attachments/assets/1be178d8-768b-47eb-a6fe-73269f730d17)

![image](https://github.com/user-attachments/assets/b518c413-c1de-46d0-9032-29c678857890)

so we need to create the kustomize.yaml file in the folder. and then we need to `kustomize build k8s/`, this will give us the final config.
- to apply the config as well: `kustomize build k8s/ | kubectl apply -f -`
- to delete stuff from kustomize: `kustomize build k8s/ | kubectl delete -f -`
- if you want to do it using kubectl only, then `kubectl apply -k k8s/` or replace apply by delete.

if we have a lot of folders to work with, we don't want to go inside each dir and apply configs, for that we can use kustomize:
![image](https://github.com/user-attachments/assets/688dc0c6-4677-410d-b492-6796098b413e)

now we can simply do `kustomize build k8s/ | kubectl apply -f -`

And when we have more folders and our kustomize.yaml looks very lengthy, we can simple create kustomize for each dir :

![image](https://github.com/user-attachments/assets/3608d60d-5534-4095-8f1f-6666b4e5e490)

Transformers: these are used to add some stuff to all the imported configs by kustomize.

![image](https://github.com/user-attachments/assets/476074f4-620a-429e-95cb-506a7f127020)

e.g.:
```yaml
labels:
  abc: xyz

namespace: dev

namePrefix: abc
nameSuffix: -dev

commonAnnotations:
  abc: xyz
```

Other than these we also have image transformer, it will change the image of all the containers with the name nginx:

![image](https://github.com/user-attachments/assets/2fa93359-32e0-43e6-a0df-2371aca47893)

```yaml
images:
  - name: [OLD IMAGE] #don't confuse it will container name. 
    newName: [NEW IMAGE] 
```
or we can also change the image tag

```yaml
images:
  name: [OLD IMAGE]
  newName: [NEW IMAGE]
  newTag: [Tag e.g. "1.24"] 
```

this will change nginx -> nginx:1.24

Other that transformers, we also have Patches that are much more surgical. for this we need:
1. **Operation**: add, remove, replace
2. **Target**
3. **Value:** for add or replace

And patching is of two types - inline and seperate file (which is also present in k8s docs)

1. Inline:

![image](https://github.com/user-attachments/assets/99d838d0-0e22-4766-921d-8c93f17edb6a)

Target means we will apply this to all the objects that have those configurations.

for list, its a bit different:

![image](https://github.com/user-attachments/assets/f5f888be-b3a0-4041-8c34-85a8d1f2a4af)

![image](https://github.com/user-attachments/assets/54df0f23-84f5-46d8-81cf-2d90f121c5ab)
(- means append at the end)


2. Seperate file:

![image](https://github.com/user-attachments/assets/057365e3-3848-4071-94cd-cb96909e3037)

### Overlays

![image](https://github.com/user-attachments/assets/56b4e493-7790-4d6c-9fad-03ceee531412)

### Components

![image](https://github.com/user-attachments/assets/795ff12b-1c05-47fb-8d92-d2c80294f18c)
