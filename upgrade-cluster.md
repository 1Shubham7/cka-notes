Draining means emptying the node to update it + corden.
Corden means mark the node as Unschedulable. 

![image](https://github.com/user-attachments/assets/46c7354b-5432-4f23-a1d5-a938ce4d7791)

![image](https://github.com/user-attachments/assets/6fa32aab-439c-48d4-b7ef-22a01892d685)

- We can't upgrade 2 minor versions ahead. we first upgrade 1.28.2 -> 1.29.3 -> 1.30.1.
- Also at a time, kubernetes only gives support for 3 releases.

![image](https://github.com/user-attachments/assets/1e97f215-e424-43e2-bbef-236dcc94120c)

so 1.28.2 will go out of support (there won't be any new bug fixes and enhancements).

There are multiple stratigies to upgrade clusters:
1. all worked nodes at once
2. rolling update
3. blue green approach: create new worker nodes with upgraded version and connect them to control plane and delete prev nodes
