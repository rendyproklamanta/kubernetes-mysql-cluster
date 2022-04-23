# Run MySql with kubernetes cluster

> Ref : https://github.com/mysql/mysql-operator

<br>

## ❕❗❕ THIS IS NOT FOR PRODUCTION USE ❕❗❕ <br><br> You can use Percona XtraDB Cluster for Production : https://gist.github.com/rendyproklamanta/a8219be8517a25227908c4e7a0d9d925

<br>

- Deploy prerequisite yaml

```
$ kubectl --kubeconfig=D:\kubeconfig\vultr\test.yaml apply -f https://raw.githubusercontent.com/mysql/mysql-operator/trunk/deploy/deploy-crds.yaml
$ kubectl --kubeconfig=D:\kubeconfig\vultr\test.yaml apply -f https://raw.githubusercontent.com/mysql/mysql-operator/trunk/deploy/deploy-operator.yaml
```

- Set root password generic

```
kubectl --kubeconfig=D:\kubeconfig\vultr\test.yaml create secret generic mysql-root-password --from-literal=rootUser=root --from-literal=rootHost=% --from-literal=rootPassword="<insert_your_password>"
```

- Deploy cluster

```
kubectl --kubeconfig=D:\kubeconfig\vultr\test.yaml apply -f deploy.yaml
```

- Show cluster running and pvc

```
$ kubectl --kubeconfig=D:\kubeconfig\vultr\test.yaml get pvc
$ kubectl --kubeconfig=D:\kubeconfig\vultr\test.yaml get innodbcluster
```

- Test running mysql cluster in local PC

```
kubectl port-forward service/mycluster mysql
```

- Open navicat/mysql workbench

```
Host : 127.0.0.1
Port : 6446
User : root
Pass : 123qwe
```

- Delete Cluster

```
$ kubectl --kubeconfig=D:\kubeconfig\vultr\test.yaml delete pvc datadir-mycluster-0 ...
$ kubectl --kubeconfig=D:\kubeconfig\vultr\test.yaml delete innodbcluster mycluster
$ kubectl --kubeconfig=D:\kubeconfig\vultr\test.yaml delete svc mycluster mycluster-instances
```
