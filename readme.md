# Notes from KubeCon Kubernetes Operators Workshop by Red Hat

Contents

- [Tutorials](./tutorials)
    - The original workshop material
- [Repositories](./repos)
    - Repositories linked from this repository

## Setup Linked Repositories

These are included as Git submodules, initialise with:

```sh
git submodule init
git submodule sync
git submodule update --init
```

## Setup MiniKube

### 1. Install MiniKube

#### MacOS

Install Docker for Mac:

```sh
open https://hub.docker.com/editions/community/docker-ce-desktop-mac
```

Install the HyperKit driver for Docker:

```sh
brew install docker-machine-driver-hyperkit
```

Install MiniKube:

```
brew cask install minikube
```

### 2. Start MiniKube

```sh
minikube --vm-driver=hyperkit start
```

### 3. Verify MiniKube works

```sh
minikube status
```

# Links/References

1. [OpenShift Training Material](https://learn.openshift.com/training/kubecon)
2. [Instructor Training Material](http://operator:coreostrainme@workshop.coreostrain.me)
3. [Kubernetes API Definition](https://github.com/kubernetes/api)
4. [Kubernetes API Machinery](https://github.com/kubernetes/apimachinery)
5. [Kubernetes Client Go](https://github.com/kubernetes/client-go)
6. [Operator Framework](https://github.com/operator-framework)
7. [Operator SDK](https://github.com/operator-framework/operator-sdk)
