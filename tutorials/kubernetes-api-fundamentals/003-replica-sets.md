# Replica Sets

Get a list of all pods in the myproject Namespace:

```sh
oc get pods -n myproject
```

Create a ReplicaSet object manifest file:

```sh
cat > replica-set.yaml <<EOF
apiVersion: extensions/v1beta1
kind: ReplicaSet
metadata:
  name: myfirstreplicaset
  namespace: myproject
spec:
  selector:
    matchLabels:
     app: myfirstapp
  replicas: 3
  template:
    metadata:
      labels:
        app: myfirstapp
    spec:
      containers:
        - name: nodejs
          image: openshiftkatacoda/blog-django-py
EOF
```

Create the ReplicaSet:

```sh
oc apply -f replica-set.yaml
```

In a new terminal window, select all pods that match app=myfirstapp:

```sh
oc get pods -l app=myfirstapp --show-labels -w
```

Delete the pods and watch new ones spawn:

```sh
oc delete pod -l app=myfirstapp
```

Imperatively scale the ReplicaSet to 6 replicas:

```sh
oc scale replicaset myfirstreplicaset --replicas=6
```

Imperatively scale down the ReplicaSet to 3 replicas:

```sh
oc scale replicaset myfirstreplicaset --replicas=3
```

The oc scale command interacts with the /scale endpoint:

```sh
curl -X GET http://localhost:8001/apis/extensions/v1beta1/namespaces/myproject/replicasets/myfirstreplicaset/scale
```

Use the PUT method against the /scale endpoint to change the number of replicas to 5:

```sh
curl  -X PUT localhost:8001/apis/extensions/v1beta1/namespaces/myproject/replicasets/myfirstreplicaset/scale -H "Content-type: application/json" -d '{"kind":"Scale","apiVersion":"extensions/v1beta1","metadata":{"name":"myfirstreplicaset","namespace":"myproject"},"spec":{"replicas":5}}'
```

You can also get information regarding the pod by using the GET method against the /status endpoint

```sh
curl -X GET http://localhost:8001/apis/extensions/v1beta1/namespaces/myproject/replicasets/myfirstreplicaset/status
```

The status endpoint's primary purpose is to allow a controller (with proper RBAC permissions) to send a PUT method along with the desired status.
