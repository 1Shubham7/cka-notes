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

1. Create a nginx pod called nginx-resolver using image nginx, expose it
internally with a service called nginx-resolver-service. Test that you are
able to look up the service and pod names from within the cluster. Use the
image: busybox: 1.28 for dns lookup. Record results in nginx.svc and
nginx.pod

`k run nginx-resolver --image=nginx`

`k expose pod/nginx-resolver --port=80 --name=nginx-resolver-service --type=ClusterIP`

`k run busybox --image=busybox:1.28 --command sleep 4000`

`k exec busybox -it -- nslookup nginx-resolver-service`

then you will get Fully Qualified Domain Name for nginx-resolver-service, use that instead:

`k exec busybox -it -- nslookup nginx-resolver-service.default.svc.cluster.local  > nginx.svc`

and

`k exec busybox -it -- nslookup 192.168.1.4 > nginx.pod`
