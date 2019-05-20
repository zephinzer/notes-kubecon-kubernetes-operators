# Apply the CockroachDB Custom Resource

Open a new terminal window and navigate to the cockroachdb-operator top-level directory:

```sh
cd $GOPATH/src/github.com/redhat/cockroachdb-operator
```

Before applying the CockroachDB Custom Resource, observe the CockroachDB Helm Chart values.yaml:

[CockroachDB Helm Chart Values.yaml file](https://github.com/helm/charts/blob/master/stable/cockroachdb/values.yaml)

Update the CockroachDB Custom Resource at go/src/github.com/redhat/cockroachdb-operator/deploy/crds/charts_v1alpha1_cockroachdb_cr.yaml with the following values:

```yaml
    spec.Replicas: 1
    spec.Storage: 1Gi
    spec.StorageClass: local-storage
```

```yaml
apiVersion: charts.helm.k8s.io/v1alpha1
kind: Cockroachdb
metadata:
  name: example
spec:
  Replicas: 1
  Storage: "1Gi"
  StorageClass: local-storage
```

After updating the CockroachDB Custom Resource with our desired spec, apply it to the cluster:

```sh
oc apply -f deploy/crds/charts_v1alpha1_cockroachdb_cr.yaml
```

Confirm that the Custom Resource was created:

```sh
oc get cockroachdb
```

It may take some time for the environment to pull down the CockroachDB container image. Confirm that the Stateful Set was created:

```sh
oc get statefulset
```

Confirm that the Stateful Set's pod is currently running:

```sh
oc get pods -l chart=cockroachdb-2.1.1
```

Confirm that the CockroachDB "internal" and "public" ClusterIP Service were created:

```sh
oc get services
```
