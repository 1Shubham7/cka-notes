Firstly, how the website and server communicate:

![image](https://github.com/user-attachments/assets/efa1526a-ea74-4ff8-a2af-d3798e2496a8)

To explain in detail:

1. DNS Resolution
2. Establish a TCP Connection
![image](https://github.com/user-attachments/assets/698428bd-b367-42ba-ac46-c82ddd52c6fa)

3. Initiate the TLS Handshake
![image](https://github.com/user-attachments/assets/c6f70f31-01fe-4ef0-afd7-dfab5b06d7c6)

4. Communication is encrypted, now you can send HTTP req.

**Public Key:** tells who you are
**Private Key:** proves who you are + decryption

- all the certificates in K8s are stored at `/etc/kubernetes/pki`

In Kubernetes, communication between these components also encrypted via CA certificates:

![image](https://github.com/user-attachments/assets/5cd1213a-7286-40f9-b0d8-3f628d915ff3)

