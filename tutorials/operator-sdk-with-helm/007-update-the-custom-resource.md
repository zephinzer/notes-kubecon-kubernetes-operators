# Update the CockroachDB Custom Resource

Let's now update the CockroachDB example Custom Resource and increase the desired number of replicas to 3:

```sh
oc patch cockroachdb example --type='json' -p '[{"op": "replace", "path": "/spec/Replicas", "value":3}]'
```

Verify that the CockroachDB Stateful Set is creating two additional pods:

```sh
oc get pods -l chart=cockroachdb-2.1.1
```

The CockroachDB UI should now reflect these additional nodes as well.
