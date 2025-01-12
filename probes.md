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

for e.g. if you container takes 10 sec to start, then till that 10 secs users would get `503` Service Unavailable error, readiness probe ensures that the container will be able to accept request only after the readiness probe is passed (and it won't probe container unless it is started). If the readiness probe fails, the container is marked as not ready, and Kubernetes removes it from the list of endpoints of the Service (Pod will no longer receive traffic routed through the Service).

### 3. Startup Probe

Startup probes are like readiness probe for containers (legacy applications or those requiring heavy initialization) that take a long time to start. They allow Kubernetes to delay the execution of liveness and readiness probes until the application is ready to handle requests.

Kubernetes runs the startup probe on a container until it succeeds or its failure threshold is reached. During this time, liveness and readiness probes are not executed. Once the startup probe succeeds, Kubernetes disables the startup probe and begins executing liveness and readiness probes as usual. If the startup probe fails, Kubernetes treats the container as failed and follows the pod restart policy.

>> Why not just use Readiness probe?

With a startup probe, liveness and readiness probes are disabled until the startup probe succeeds. This prevents Kubernetes from prematurely marking the container as unhealthy or routing traffic to it. With only a readiness probe, Kubernetes may attempt to route traffic to the container once it starts, even if it’s not fully initialized, leading to errors or degraded performance. startup probe ensures that the container is started and initialized while readiness probe ensures that its just ready even if not initialized.

in CKA, get the syntax from docs.
