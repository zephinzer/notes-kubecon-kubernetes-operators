# Creating the Subscription

Let's begin my creating a new project called myproject.

```sh
oc new-project myproject
```

Create a Subscription manifest for the Etcd Operator. Ensure the Approval is set to Manual.

```sh
cat > etcd-alpha-subscription.yaml <<EOF
apiVersion: operators.coreos.com/v1alpha1
kind: Subscription
metadata:
  name: etcd
  namespace: myproject 
spec:
  channel: alpha
  name: etcd
  source: rh-operators
  installPlanApproval: Manual
EOF
```

Create the Subscription.

```sh
oc create -f etcd-alpha-subscription.yaml
```

Verify the Subscription and InstallPlan have been created.

```sh
oc get subscription
oc get installplan
```
