# Creating the Custom Resource

Create the etcdCluster manifest.

```sh
cat > etcd-cluster.yaml <<EOF
apiVersion: etcd.database.coreos.com/v1beta2
kind: EtcdCluster
metadata:
  name: example-etcd-cluster
spec:
  size: 3
EOF
```

Create the etcd-cluster.

```sh
oc create -f etcd-cluster.yaml
```

Confirm the cluster has been created:

```sh
oc get etcdcluster
oc get pods
```
