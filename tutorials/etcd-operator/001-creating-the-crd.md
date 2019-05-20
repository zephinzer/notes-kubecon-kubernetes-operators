# Creating the Custom Resource Definition (CRD)

Let's begin my creating a new project called myproject:

```sh
oc new-project myproject
```

Create the Custom Resource Definition (CRD) for the Etcd Operator:

```sh
cat > etcd-operator-crd.yaml<<EOF
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: etcdclusters.etcd.database.coreos.com
spec:
  group: etcd.database.coreos.com
  names:
    kind: EtcdCluster
    listKind: EtcdClusterList
    plural: etcdclusters
    shortNames:
    - etcdclus
    - etcd
    singular: etcdcluster
  scope: Namespaced
  version: v1beta2
  versions:
  - name: v1beta2
    served: true
    storage: true
EOF
```

```sh
oc create -f etcd-operator-crd.yaml
```

Verify the CRD was successfully created.

```sh
oc get crd
```
