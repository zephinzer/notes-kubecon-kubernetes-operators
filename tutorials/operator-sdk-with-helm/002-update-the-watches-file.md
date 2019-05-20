# Update the Watches File

The watches.yaml file maps a Group, Version, and Kind to a specific Helm Chart. Observe the contents of the watches.yaml:

```sh
cat watches.yaml
```

Create a symlink that targets the Cockroachdb Helm chart in the cockroachdb-operator project directory.

```sh
mkdir -p /opt/helm/helm-charts
ln -s /root/tutorial/go/src/github.com/redhat/cockroachdb-operator/helm-charts/cockroachdb/ /opt/helm/helm-charts/
```
