# Approving the InstallPlan

Modify the InstallPlan and set approved to true.

```sh
oc edit InstallPlan
```

Once the InstallPlan is set to true, you will see the newly provisioned ClusterServiceVersion, ClusterResourceDefinition, Role and RoleBindings, Service Accounts, and etcd-operator Deployment.

```sh
oc get clusterserviceversion
oc get crd
oc get sa
oc get roles
oc get rolebindings
oc get deployments
```
