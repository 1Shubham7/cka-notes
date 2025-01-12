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
