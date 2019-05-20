# Clean Up

Delete the CockroachDB cluster and all associated resources by deleting the example Custom Resource:

```sh
oc delete cockroachdb example
```

Verify that the Stateful Set, pods, and services are removed:

```sh
oc get statefulset
oc get pods
oc get services
```
