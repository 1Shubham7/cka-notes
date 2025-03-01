## Networking

- `ip address show type bridge`

This will give us the interface/bridge of that node. `show` means show specific thing, `type bridge` means type is bridge. 

- If you were to ping google from the controlplane node, which route does it take? (What is the IP address of the Default Gateway?)

for this we will do `ip route` :

```
default via 169.254.1.1 dev eth0 
169.254.1.1 dev eth0 scope link 
172.17.0.0/24 dev cni0 proto kernel scope link src 172.17.0.1 
172.17.1.0/24 via 172.17.1.0 dev flannel.1 onlink
```

so the default one is 169...

## Ingress

you can expose your application to the outside world using service of type NodePort or LoadBalancer but they are not ideal to serve your application to customers. NodePort is used within org, and load balancer service requires a Load Balancer from the cloud providers.

- An Ingress is an Kubernetes  object that manages external access to services within a cluster, typically HTTP and HTTPS traffic.

- NodePort: Exposes a service on every node’s IP, but uses high-numbered ports. LoadBalancer: Creates a cloud provider’s external load balancer, but each service gets a separate one (costly). Instead, Ingress provides a smarter way:
1. It uses a single entry point (a domain like example.com).
2. It routes requests to different services based on the URL path or hostname.
3. It supports HTTPS (TLS) and load balancing automatically.

Example: You have two apps running:

app1 on app1-service
app2 on app2-service

example.com/app1 → Goes to app1-service
example.com/app2 → Goes to app2-service

For this you will need:

```yaml
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /app1
        pathType: Prefix
        backend:
          service:
            name: app1-service
            port:
              number: 80
      - path: /app2
        pathType: Prefix
        backend:
          service:
            name: app2-service
            port:
              number: 80
```

### Ingress controller
So Ingress controller configures a load balancer using the rules written in Ingress. ex. F5, Kong etc.

1. You define an Ingress resource (a set of rules) that tells Kubernetes how to route traffic.
2. An Ingress Controller (like NGINX) listens to those rules and actually handles traffic.
