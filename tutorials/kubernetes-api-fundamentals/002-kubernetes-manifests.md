# Kubernetes Manifests

Let's begin my creating a new project called myproject:

```sh
oc new-project myproject
```

Create a new pod manifest that specifies two containers:

```sh
cat > pod-multi-container.yaml <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: my-two-container-pod
  namespace: myproject
  labels:
    environment: dev
spec:
  containers:
    - name: server
      image: nginx:1.13-alpine
      ports:
        - containerPort: 80
          protocol: TCP
    - name: side-car
      image: alpine:latest
      command: ["/usr/bin/tail", "-f", "/dev/null"]
  restartPolicy: Never
EOF
```

Create the pod by specifying the manifest:

```sh
oc create -f pod-multi-container.yaml
```

View the detail for the pod and look at the events:

```sh
oc describe pod my-two-container-pod
```

Let's first execute a shell session inside the server container by using the -c flag:

```sh
oc exec -it my-two-container-pod -c server -- /bin/sh
```

Run some commands inside the server container:

```sh
ip address
netstat -ntlp
hostname
ps
exit
```

Let's now execute a shell session inside the side-car container:

```sh
oc exec -it my-two-container-pod -c side-car -- /bin/sh
```

Run the same commands in side-car container. Each container within a pod runs it's own cgroup, but shares IPC, Network, and UTC (hostname) namespaces:

```sh
ip address
netstat -ntlp
hostname
exit
```
