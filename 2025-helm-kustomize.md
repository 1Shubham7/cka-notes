### HELM

To install helm: `sudo snap install helm --classic`

- When a helm chart is applied, a single release of the app is installed to the cluster (helm charts are nothing but `.yaml` files). and we can use `values.yaml` file to customize the helm charts. `Chart.yaml` has info about the charts. if apiversion in chart.yaml is v1 or not specified then it is helm 2. If it is v2, then it is helm3.

- to add the repo: `helm repo add [NAME] [LINK]
- to install chart: `helm install [RELEASE-NAME] [CHART]`
- to delere: `helm uninstall [RELEASE-NAME]`
- to list releases : `helm list` (Releases are nothing but apps, not calling them apps because we can install multiple releases of a single helm chart or application.
- Use `--set abc="xyz"` or `--values v.yaml` to change the values while `helm install`. OR:
- do `helm pull --untar [CHART]` and changes to the values.yaml and then install: `helm install [RELEASE-NAME] [DIR_PATH]`
-  `helm search [hub or repo] [CHART_NAME] ` to search for charts  

![image](https://github.com/user-attachments/assets/65810fa2-61c4-47b6-b5a8-6576f0bac018)

![image](https://github.com/user-attachments/assets/7a4f91c9-c6b9-4261-8168-93fc005ef3cb)

- 
