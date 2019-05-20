# Creating the Service Account, Role, and RoleBinding

Create a dedicated Service Account responsible for running the Etcd Operator:

```sh
cat > etcd-operator-sa.yaml<<EOF
apiVersion: v1
kind: ServiceAccount
metadata:
  name: etcd-operator-sa
EOF
```

```sh
oc create -f etcd-operator-sa.yaml
```

Verify the Service Account was successfully created:

```sh
oc get sa
```

Create the Role that the etcd-operator-sa Service Account will need for authorization to perform actions against the Kubernetes API:

```sh
cat > etcd-operator-role.yaml<<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: etcd-operator-role
rules:
- apiGroups:
  - etcd.database.coreos.com
  resources:
  - etcdclusters
  - etcdbackups
  - etcdrestores
  verbs:
  - '*'
- apiGroups:
  - ""
  resources:
  - pods
  - services
  - endpoints
  - persistentvolumeclaims
  - events
  verbs:
  - '*'
- apiGroups:
  - apps
  resources:
  - deployments
  verbs:
  - '*'
- apiGroups:
  - ""
  resources:
  - secrets
  verbs:
  - get
EOF
```

```sh
oc create -f etcd-operator-role.yaml
```

Verify the Role was successfully created:

```sh
oc get roles
```

Create the RoleBinding to bind the etcd-operator-role Role to the etcd-operator-sa Service Account:

```sh
cat > etcd-operator-rolebinding.yaml<<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: etcd-operator-rolebinding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: etcd-operator-role
subjects:
- kind: ServiceAccount
  name: etcd-operator-sa
  namespace: myproject
EOF
```

```sh
oc create -f etcd-operator-rolebinding.yaml
```

Verify the RoleBinding was successfully created:

```sh
oc get rolebindings
```
