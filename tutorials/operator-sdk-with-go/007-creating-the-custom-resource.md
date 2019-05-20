# Creating the Custom Resource

In a new terminal, inspect the Custom Resource manifest:

```sh
cd tutorial/go/src/github.com/redhat/podset-operator/
cat deploy/crds/app_v1alpha1_podset_cr.yaml
```

Ensure your kind: PodSet Custom Resource (CR) is updated with spec.replicas:

```yaml
apiVersion: app.example.com/v1alpha1
kind: PodSet
metadata:
  name: example-podset
spec:
  replicas: 3
```

Deploy your PodSet Custom Resource to the live OpenShift Cluster:

```sh
oc create -f deploy/crds/app_v1alpha1_podset_cr.yaml
```

Verify the PodSet operator has created 3 pods:

```sh
oc get pods
```

Verify that status shows the name of the pods currently owned by the PodSet:

```sh
oc get podset example-podset -o yaml
```

Increase the number of replicas owned by the PodSet:

```sh
oc patch podset example-podset --type='json' -p '[{"op": "replace", "path": "/spec/replicas", "value":5}]'
```
