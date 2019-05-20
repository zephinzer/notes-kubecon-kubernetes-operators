# Setting up the UI

To access the Operator Lifecycle Manager via the UI, we will run a local copy of the UI found in the container image quay.io/openshift/origin-console:latest.

The local console proxy utilizes the `system:serviceaccount:kube-system:default` Service Account to access all resources.

We will first grant this Service Account cluster-admin access. DO NOT DO THIS IN PRODUCTION.

```sh
oc adm policy add-cluster-role-to-user cluster-admin system:serviceaccount:kube-system:default
```

Replace the Operator-centric Origin console container image latest tag with v3.11.0.

```sh
sed -i 's|latest|v3.11.0|g' ./operator-lifecycle-manager/scripts/run_console_local.sh
```

Serve up the Operator-centric Origin console locally.

```sh
./operator-lifecycle-manager/scripts/run_console_local.sh
```

To access the UI, visit https://2887723560-9000-916529223-training1.environments.katacoda.com
