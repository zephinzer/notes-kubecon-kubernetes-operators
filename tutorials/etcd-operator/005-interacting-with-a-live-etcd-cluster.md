# Interacting with a Live Etcd Cluster

Let's now create another pod and attempt to connect to the etcd cluster via etcdctl:

```sh
oc run etcdclient --image=busybox busybox --restart=Never -- /usr/bin/tail -f /dev/null
```

Access the pod:

```sh
oc rsh etcdclient
```

Install the Etcd Client:

```sh
wget https://github.com/coreos/etcd/releases/download/v3.1.4/etcd-v3.1.4-linux-amd64.tar.gz
tar -xvf etcd-v3.1.4-linux-amd64.tar.gz
cp etcd-v3.1.4-linux-amd64/etcdctl .
```

Set the etcd version and endpoint variables:

```sh
export ETCDCTL_API=3
export ETCDCTL_ENDPOINTS=example-etcd-cluster-client:2379
```

Attempt to write a key/value into the Etcd cluster:

```sh
./etcdctl put operator sdk
./etcdctl get operator
```

Exit out of the client pod:

```sh
exit
```
