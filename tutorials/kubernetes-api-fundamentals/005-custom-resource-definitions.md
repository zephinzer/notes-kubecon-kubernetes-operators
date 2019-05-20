# Custom Resource Definitions

Begin by running a proxy to the Kubernetes API server:

```sh
oc proxy --port=8001
```

Open up another terminal by clicking the + button and select Open New Terminal.

Let's create a new Custom Resource Definition (CRD) object manifest for Postgres:

```sh
cat >> postgres-crd.yaml <<EOF
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: postgreses.rd.example.com
spec:
  group: rd.example.com
  names:
    kind: Postgres
    listKind: PostgresList
    plural: postgreses
    singular: postgres
    shortNames:
    - pg
  scope: Namespaced
  version: v1alpha1
EOF
```

Create the CRD resource object:

```sh
oc create -f postgres-crd.yaml
```

You should now see the Kubernetes API reflect a brand new api group called rd.example.com:

```sh
curl http://localhost:8001/apis | jq .groups[].name
```

This will also be reflected in the oc api-versions command:

```sh
oc api-versions
```

Within the rd.example.com group there will be an api version v1alpha1 (per our CRD resource object). The database resource resides here.

```sh
curl http://localhost:8001/apis/rd.example.com/v1alpha1 | jq
```

Notice how oc now recognize postgres as a present resource (although there will be no current resource objects at this time).

```sh
oc get postgres
```

Let's create a new Custom Resource (CR) object manifest for the database:

```sh
cat >> wordpress-database.yaml <<EOF
apiVersion: "rd.example.com/v1alpha1"
kind: Postgres
metadata:
  name: wordpressdb
spec:
  user: postgres
  password: postgres
  database: primarydb
  nodes: 3
EOF
```

Create the new object:

```sh
oc create -f wordpress-database.yaml
```

Verify the resource was created:

```sh
oc get postgres
```

View the details about the wordpressdb object:

```sh
oc get postgres wordpressdb -o yaml
```
