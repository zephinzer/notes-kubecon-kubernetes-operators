# Deployments/Finalizers

Create a manifest for a Deployment with a Finalizer:

```sh
cat > finalizer-test.yaml<<EOF
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: finalizer-test
  namespace: myproject
  labels:
    app: finalizer-test
  finalizers:
    - finalizer.extensions/v1beta1  
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: finalizer-test
    spec:
      containers:
        - name: hieveryone
          image: openshiftkatacoda/blog-django-py
          imagePullPolicy: Always
          ports:
            - name: helloworldport
              containerPort: 8080
EOF
```

Create the Deployment.

```sh
oc create -f finalizer-test.yaml
```

Verify the Deployment has been created.

```sh
oc get deploy
```

Verify the ReplicaSet has been created:

```sh
oc get replicaset
```

Verify the pods are running:

```sh
oc get pods
```

Attempt to delete the Deployment.

```sh
oc delete deployment finalizer-test
```

Open up another terminal by clicking the + button and select Open New Terminal.

Observe the Deployment still exits and has been updated with the deletionGracePeriodSeconds and deletionTimestamp fields.

```sh
oc get deployment finalizer-test -o yaml | grep 'deletionGracePeriodSeconds\|deletionTimestamp'
```

Attempt to scale the Deployment up and down. Although status is updated, pods will not be created/deleted:

```sh
oc scale deploy finalizer-test --replicas=5
oc scale deploy finalizer-test --replicas=1
```

```sh
oc get deploy
oc get pods
```

Update the Deployment with the Finalizer value unset.

```sh
cat > finalizer-test-remove.yaml<<EOF
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: finalizer-test
  namespace: myproject
  labels:
    app: finalizer-test
  finalizers:
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: finalizer-test
    spec:
      containers:
        - name: hieveryone
          image: openshiftkatacoda/blog-django-py
          imagePullPolicy: Always
          ports:
            - name: helloworldport
              containerPort: 8080
EOF
```

Replace the Deployment.

```sh
oc replace -f finalizer-test-remove.yaml
```

The Deployment will now be deleted.

```sh
oc get deploy
oc get pods
```
