# Run MySQL with kubernetes cluster

https://gist.github.com/rendyproklamanta/a8219be8517a25227908c4e7a0d9d925

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