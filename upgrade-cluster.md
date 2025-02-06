Draining means emptying the node to update it + corden.
Corden means mark the node as Unschedulable. 

![image](https://github.com/user-attachments/assets/46c7354b-5432-4f23-a1d5-a938ce4d7791)

![image](https://github.com/user-attachments/assets/6fa32aab-439c-48d4-b7ef-22a01892d685)

- We can't upgrade 2 minor versions ahead. we first upgrade 1.28.2 -> 1.29.3 -> 1.30.1.
- Also at a time, kubernetes only gives support for 3 releases.
- Also if our kube API server is at 1.29.1 then the our controller manager or kube scheduller can at max be 1 version behind. and other components (Kubelet, Kubectl) can be 2 version behind 

![image](https://github.com/user-attachments/assets/1e97f215-e424-43e2-bbef-236dcc94120c)

so 1.28.2 will go out of support (there won't be any new bug fixes and enhancements).

There are multiple stratigies to upgrade clusters:
1. all worked nodes at once
2. rolling update
3. blue green approach: create new worker nodes with upgraded version and connect them to control plane and delete prev nodes

### Step 1. check your OS. 

`cat etc/os-release` and you will find your OS. mine was ubuntu

### Step 2. Go to docs you will find this command:

```
sudo apt update
sudo apt-cache madison kubeadm
```

this will tell you the versions you can upgrade to. also verify with this:

`sudo kubeadm upgrade plan`

Step 3. Upgrade Kubeadm:

```
sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm='1.29.13-*' && \
sudo apt-mark hold kubeadm
```
