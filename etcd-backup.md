## etcd backup

the etcd yaml manifest is present in the `etc/kubernetes/manifests` dir.To backup etcd, we need `etcdctl`:

### firstly search in k8s docs, there is a tutorial. 

Step 1. `sudo apt  install etcd-client` (also if you don't remember how to install anything, simply type that command and apt will give you the details.)

Step 2. write this env variable everytime or export it `export ETCDCTL_API=3`. 3 is the version of ectdctl. but still create that variable everytime, create a snapshot/backup:

```
sudo ETCDCTL_API=3 etcdctl --endpoints=https:
//127.0.0.1:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --
key=/etc/kubernetes/pki/etcd/server.key snapshot save /opt/etcd-backup.db
Snapshot saved at /opt/etcd-backup.db
```

you don't have to remember the command, you can find that in docs, but make sure to remember the snapshot has to be saved at `/opt/etc-backup.db`

Step 3. now restore using etcdutil command, it will be installed in cka, but I am using this:

`sudo ETCDCTL_API=3 etcdctl --data-dir=/var/lib/etcd-restore snapshot restore /opt/etcd-backup.db`

remember we are saving the restore in `/var/lib/etcd-restore`

Step 4. now vim into the ectd.yaml and change one argument and one volument mount path (remember this yo uwill not find this in docs):

```
--data-dir=/var/lib/etcd-restore
.
.
.
volumeMounts:
    - mountPath: /var/lib/etcd-restore
.
.
.
volumeMounts:
    - mountPath: /var/lib/etcd-restore
```
(there are two volumemounts that we need to change)

Step 5. Now we just have to restart api server components :

`mv * /tmp`  ...

and then also restart these:

`systemctl restart kubelet`
`systemctl daemon-reload`

Step 6. wait for some time, and once the services are up and running, check the etcd configuration and see if the data-dir and volume mount is changed.
