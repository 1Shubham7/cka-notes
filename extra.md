- Get all pods with selector

`k get pod --selector env=dev`

- number of pods with selector env=dev:

`k get pod --selector env=dev | wc -l` but this will also count the header, so subtract 1, otherwise:

`k get pod --selector env=dev --no-headers | wc -l`

To install Metrics server add this in args : `--kubelet-insecure-tls`

How many cluster are present: `k config get-contexts`

Mac address of node - `ip link show` and the mac address will be under eth0

- how to identify the authorization modes configured on the cluster:

just look into kube-apiserver yaml you will see a flag:

`--authorization-mode=Node,RBAC`
