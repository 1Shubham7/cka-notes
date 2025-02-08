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

`sudo su -` to become root user
