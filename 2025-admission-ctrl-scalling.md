## Admission Controllers

to add a default admission controller: 
just go to kube-apiserver.yaml and add it in `- --enable-admission-plugins=NodeRestriction` and to disable any admission controller, add this: `- --disable-admission-plugins=DefaultStorageClass`

- to see all the current admission controllers:

`kubectl exec -it kube-apiserver-controlplane -n kube-system -- kube-apiserver -h | grep enable-admission-plugins`

## Autoscalling

![image](https://github.com/user-attachments/assets/6b5553c5-a50b-4a03-9b55-01332a9f162a)

Horizontal scalling: increasing the no. of node or pods
Vertical scalling: increasing the resources on node or pods

![image](https://github.com/user-attachments/assets/5ea17809-ceca-4585-9090-a14b93fa2bd0)

1. **Horizontal Pod autoscaller:** it will observe the pod metrics, automatically add pods and remove pods. (u need a metrics server before this)

`kubectl autoscale deploy my-app --cpu-percent=50 --min=1 --max=10` if cpu-usage goes beyond 50% it will scale

`kubectl get hpa`

2. **Vertical Pod Autoscaller:** it does'nt come built it, so we install it first. There is also no imperitive command, we create a yaml file

![image](https://github.com/user-attachments/assets/94edc0b3-26f4-4ba8-aaf8-eb98abd913f6)
