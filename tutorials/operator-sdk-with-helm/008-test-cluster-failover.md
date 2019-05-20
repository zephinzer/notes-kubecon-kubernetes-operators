# Test CockroachDB Cluster Failover

If any CockroachDB member fails it gets restarted or recreated automatically by the Kubernetes infrastructure, and will rejoin the cluster automatically when it comes back up. You can test this scenario by killing any of the pods:

```sh
oc delete pods -l chart=cockroachdb-2.1.1
```

Watch the pods respawn:

```sh
oc get pods -l chart=cockroachdb-2.1.1
```

Confirm that the contents of the database still persist by connecting to the database cluster:

```sh
COCKROACHDB_PUBLIC_SERVICE=`oc get svc -o jsonpath={$.items[1].metadata.name}`
oc run -it --rm cockroach-client --image=cockroachdb/cockroach --restart=Never --command -- ./cockroach sql --insecure --host $COCKROACHDB_PUBLIC_SERVICE
```

Once you see the SQL prompt, run the following to confirm the database contents are still present:

```sql
SELECT * FROM bank.accounts;
```

Exit the SQL prompt:

```sql
\q
```
