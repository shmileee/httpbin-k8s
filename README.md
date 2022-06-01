### setup

1. create [`k3d`](https://k3d.io/v5.4.1) cluster

```bash
k3d cluster create httpbin-demo --agents 2
```

2. taint `master` node

```bash
kubectl taint nodes k3d-httpbin-demo-server-0 node-role.kubernetes.io/master=:NoSchedule
```

3. deploy

```bash
kubectl apply -f manifest.yaml
```

4. test

```bash
kubectl run -i --rm --tty busybox --image=busybox --restart=Never -- sh
```

```bash
$ wget -O - httpbin.trackunit.svc.cluster.local:8080 2>/dev/null | grep -i 'me@kennethreitz'
```

5. cleanup

```bash
kubectl delete -f manifest.yaml
```

```bash
k3d cluster delete httpbin-demo
```
