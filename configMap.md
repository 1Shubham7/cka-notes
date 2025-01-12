this is how you can specify env variables in yaml without cm:

```yaml
containers:
- name: abc
  image: nginx
  env:
  - name: FIRSTNAME
    value: "Shubham"
```

You can craete CM using this command:

```sh
kubectl create cm shubham --from-literal shubham=hi \
--from-literal abc=aaa
```

or you can create a CM from a file of variables:

```sh
kubectl create cm shubham --from-file=app.config
```

you can also create manifest by --dry-run:

`kubectl create cm my-cm --dry-run=client --from-literal abc=aaa -o yaml > g.yaml`

### Injecting CM to pod

```yaml
spec:
  containers:
  - image: nginx
    name: nginx
    envFrom:
    - configMapRef:
        name: test-cm
```

this will inject all the variables from test-cm to pod. you can find this in k8s docs as well.
