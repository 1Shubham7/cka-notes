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


## Step by step guide 

### Step 0. First go to spefic doc for the upgrade 

find your cluster version:

`k get nodes`

then go to the specifc doc for the version you want and you will find in that doc a link, first go to the link as they say and find this command:

`pager /etc/apt/sources.list.d/kubernetes.list`

then change the version there to the desired version:

`sudo vim /etc/apt/sources.list.d/kubernetes.list` (don't forget sudo otherwise it will be read only)

### Step 1. We will first upgrade kubeadm 

For that go back to the main cluster upgrade doc and First check your OS:

`cat etc/os-release` and you will find your OS. mine was ubuntu

### Step 2. Go to docs you will find this command:

find the possible kubeadm versions (always run sudo apt update, never skip, even if it comes twice)

```
sudo apt update
sudo apt-cache madison kubeadm
```

this will tell you the versions you can upgrade to. 

### Step 3. Upgrade Kubeadm:

```
sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm='1.29.13-*' && \
sudo apt-mark hold kubeadm
```

Now get a plan for your kubernetes cluster upgrade:

`sudo kubeadm upgrade plan`

### Step 4. Then upgrade the cluster:

`sudo  kubeadm upgrade apply v1.30.9`

and your version will be upgraded, this means the control plane components have been upgraded but the `k get nodes` will not show it because it shows the kubectl version.

### Step 5. Now upgrade the kubelet and kubectl

If we only have one control plane node than we can continue to drain that control plane node:

`
kubectl drain control-plane --ignore-daemonsets
`
