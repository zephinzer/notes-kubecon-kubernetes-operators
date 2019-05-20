# Setting Up OLM

The Operator Lifecycle Manager is not installed in our current Katacoda OpenShift environment. We will now install it from scratch by deploying the following objects:

- CustomResourceDefinitions:
    - `Subscription`, `InstallPlan`, `CatalogSource`, `ClusterServiceVersion`
- Namespace:
    - `openshift-operator-lifecycle-manager`
- Service Account:
    - `olm-operator-serviceaccount`
- ClusterRole:
    - `system:controller:operator-lifecycle-manager`
- ClusterRoleBinding:
    - `olm-operator-binding-openshift-operator-lifecycle-manager`
- CatalogSource:
    - `rh-operators`
- ConfigMap:
    - `rh-operators`
- Deployments:
    - `olm-operator`, `catalog-operator`, `package-server`

> Note: The initial setup of the Operator Lifecycle Manager (OLM) is a one-time task and is reserved for Kubernetes administrators with cluster-admin privileges. Once OLM is properly setup, Kubernetes administrators can then delegate Operator install privileges to non-admin Kubernetes users.

Let's get started by cloning the official OLM repository:

```sh
git clone https://github.com/operator-framework/operator-lifecycle-manager
```

Create the dedicated openshift-operator-lifecycle-manager Namespace:

```sh
oc create -f operator-lifecycle-manager/deploy/okd/manifests/0.7.2/0000_30_00-namespace.yaml
```

Verify the Namespace was successfully created:

```sh
oc get namespaces openshift-operator-lifecycle-manager
```

Create the olm-operator-serviceaccount Service Account, `system:controller:operator-lifecycle-manager` ClusterRole, and `olm-operator-binding-openshift-operator-lifecycle-manager` ClusterRoleBinding:

```sh
oc create -f operator-lifecycle-manager/deploy/okd/manifests/0.7.2/0000_30_01-olm-operator.serviceaccount.yaml
```

Verify the Service Account, ClusterRole, and ClusterRoleBinding were successfully created:

```sh
oc -n openshift-operator-lifecycle-manager get serviceaccount olm-operator-serviceaccount

oc get clusterrole system:controller:operator-lifecycle-manager

oc get clusterrolebinding olm-operator-binding-openshift-operator-lifecycle-manager
```

Create the OLM Custom Resource Definitions (Subscription, InstallPlan, CatalogSource, ClusterServiceVersion):

```sh
for num in {02..05}; do oc create -f operator-lifecycle-manager/deploy/okd/manifests/0.7.2/0000_30_$num*; done
```

Verify all four OLM CRDs are present:

```sh
oc get crds
```

Create the internal rh-operators CatalogSource and rh-operators ConfigMap which contains manifests for some popular Operators:

```sh
for num in {06,09}; do oc create -f operator-lifecycle-manager/deploy/okd/manifests/0.7.2/0000_30_$num*; done
```

Verify the CatalogSource and ConfigMap were successfully created:

```sh
oc -n openshift-operator-lifecycle-manager get catalogsource rh-operators

oc -n openshift-operator-lifecycle-manager get configmap rh-operators
```

Create the remaining OLM objects including OLM, Catalog, and Package Deployments:

```sh
for num in {10..13}; do oc create -f operator-lifecycle-manager/deploy/okd/manifests/0.7.2/0000_30_$num*; done
```

Verify all three OLM deployments were successfully created:

```sh
oc -n openshift-operator-lifecycle-manager get deployments
```

We have successfully setup the Operator Lifecycle Manager in our OpenShift cluster.
