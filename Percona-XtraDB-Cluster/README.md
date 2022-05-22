# Run MySQL with kubernetes cluster

https://gist.github.com/rendyproklamanta/a8219be8517a25227908c4e7a0d9d925

Bundle :
```
kubectl D:/kubeconfig/vultr/test.yaml apply -f https://raw.githubusercontent.com/percona/percona-xtradb-cluster-operator/v1.10.0/deploy/bundle.yaml
```

Deploy :
```
kubectl D:/kubeconfig/vultr/test.yaml apply -f deployment.yaml
```

Get Password :
```
$ kubectl D:/kubeconfig/vultr/test.yaml get secret db-cluster-secrets -o yaml

> get the root password then decode :
$ echo 'MUVtTnBDVkdJeWI4cVlraGVY' | base64 --decode
> this will show real password
```

Test running :
```
$ kubectl run -it --rm percona-client --image=percona:8.0 -- bash

$ mysql -h db-cluster-haproxy -u root -p <root_password>
```