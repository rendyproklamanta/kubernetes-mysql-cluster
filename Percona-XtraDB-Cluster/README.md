# Deploy MySQL with Percona Kubernetes Cluster

1. Bundle :
```
kubectl --kubeconfig=D:/kubeconfig/test.yaml apply -f https://raw.githubusercontent.com/percona/percona-xtradb-cluster-operator/v1.11.0/deploy/bundle.yaml
```

2. Deploy :
```
kubectl --kubeconfig=D:/kubeconfig/test.yaml apply -f deployment.yaml
```

3. Get Password :
```
$ kubectl --kubeconfig=D:/kubeconfig/test.yaml get secret db-cluster-secrets -o yaml

> get the root password then decode :
$ echo 'MUVtTnBDVkdJeWI4cVlraGVY' | base64 --decode
> this will show real password
```

4. Test running :
```
$ kubectl --kubeconfig=D:/kubeconfig/test.yaml run -it --rm percona-client --image=percona:8.0 -- bash
$ mysql -h db-cluster-haproxy -u root -p <root_password>
```

- Delete running mysql-cluster :
```
kubectl --kubeconfig=D:/kubeconfig/test.yaml get PerconaXtraDBCluster
kubectl --kubeconfig=D:/kubeconfig/vultr/test.yaml get pvc

kubectl --kubeconfig=D:/kubeconfig/test.yaml delete -f deployment.yaml
kubectl --kubeconfig=D:/kubeconfig/test.yaml delete pvc datadir-db-cluster-pxc-0/1/2 (~Remember all data in pvc will be deleted)
```
