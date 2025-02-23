### HELM

To install helm: `sudo snap install helm --classic`

- When a helm chart is applied, a single release of the app is installed to the cluster (helm charts are nothing but `.yaml` files). and we can use `values.yaml` file to customize the helm charts. `Chart.yaml` has info about the charts. if apiversion in chart.yaml is v1 or not specified then it is helm 2. If it is v2, then it is helm3.

- to install chart: `helm install [NAME] [CHART]`

![image](https://github.com/user-attachments/assets/65810fa2-61c4-47b6-b5a8-6576f0bac018)
