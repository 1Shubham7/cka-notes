### Probes

Probe means investigating something. Probes in k8s are used to determine the health and status of containers.

![image](https://github.com/user-attachments/assets/7fb76026-f9af-42f0-bbb1-474b57165180)

Types:

#### 1. Liveness Probe

it checks whether a container is alive, if check fails a specified number of times then the liveness probe fails and k8s restarts the container.

The liveness probe can use one of three mechanisms:
- HTTP GET: Sends an HTTP GET request to a specified path in the container.
- TCP Socket: Attempts to open a TCP connection on a specified port.
- Exec Command: Runs a specific command inside the container to check its health.

#### 2. Readiness Probe

for e.g. if you container takes 10 sec to start, then till that 10 secs users would get 404 error, readiness probe ensures that the container will be able to accept request only after the readiness probe is passed (and it won't probe container unless it is started). If the readiness probe fails, the container is marked as not ready, and Kubernetes removes it from the list of endpoints of the Service (Pod will no longer receive traffic routed through the Service).
