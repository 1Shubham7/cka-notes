`sudo chmod 775 a.txt`

This will change file permissions:
7 (Owner) → Full permissions (read r, write w, execute x)
7 (Group) → Full permissions (read r, write w, execute x)
5 (Others) → Read and execute only (no write)

0	---	No permissions
1	--x	Execute only
2	-w-	Write only
3	-wx	Write + Execute
4	r--	Read only
5	r-x	Read + Execute
6	rw-	Read + Write
7	rwx Full permissions

`k cluster-info` gives you info about the cluster

`sudo su -` to become root user. and then `exit` to exit.

`service kubelet status` for kubelete running or not.

`service kubelet start`

`journalctl -u kubelet` for showing up logs for the kubelet

Shift + G to go to the last line.


## JSONPATH

`k get pod -o=jsonpath='{.items[0].metadata.labels}{"\n"}'`

When using custom cols, do not specify items:

`k get pods -o='custom-columns=Good:{.status.hostIPs[0].ip}'`

Having multiple headers are like this:

`k get pods -o='custom-columns=Good:{.status.hostIPs[0].ip},Kind:{.kind}'`

`?` is used for condition and `@` is used for "each item in the list". `*` is for all.

- `first 2 elements of a list` : [0:8] , the rule is `[start: end-1: step]`
- `last element of the list` : [-1] pr [-1,0]
- {"\n"} is for new line {"\t"} is for tab

![image](https://github.com/user-attachments/assets/9456e634-b13a-45d9-8f96-7b32b5d2ff80)

// IMP: you will also find imp commands for this in the kubectl cheatsheet, remeber this
