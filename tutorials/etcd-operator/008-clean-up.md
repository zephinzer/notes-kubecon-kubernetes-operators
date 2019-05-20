# Clean Up

Delete your Etcd cluster:

```sh
oc delete etcdcluster example-etcd-cluster
```

Delete the Etcd Operator:

```sh
oc delete deployment etcd-operator
```

Delete the Etcd CRD:

```sh
oc delete crd etcdclusters.etcd.database.coreos.com
```
