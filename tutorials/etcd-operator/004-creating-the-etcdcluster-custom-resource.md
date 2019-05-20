# Creating the EtcdCluster Custom Resource (CR)

Create an Etcd cluster by referring to the new Custom Resource, EtcdCluster, defined in the Custom Resource Definition on Step 1:

```sh
cat > etcd-operator-cr.yaml<<EOF
apiVersion: etcd.database.coreos.com/v1beta2
kind: EtcdCluster
metadata:
  name: example-etcd-cluster
spec:
  size: 3
  version: 3.1.10
EOF
```

```sh
oc create -f etcd-operator-cr.yaml
```

Verify the cluster object was created:

```sh
oc get etcdclusters
```

Watch the pods in the Etcd cluster get created:

```sh
oc get pods -l etcd_cluster=example-etcd-cluster -w
```

Verify the cluster has been exposed via a ClusterIP service:

```sh
oc get services -l etcd_cluster=example-etcd-cluster
```
