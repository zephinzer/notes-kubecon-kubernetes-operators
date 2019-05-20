# Creating a New Project

Let's begin my creating a new project called myproject:

```sh
oc new-project myproject
```

Let's now create a new directory in our $GOPATH/src/ directory:

```sh
mkdir -p $GOPATH/src/github.com/redhat/
```

Navigate to the directory:

```sh
cd $GOPATH/src/github.com/redhat/
```

Create a new Go-based Operator SDK project for the PodSet:

```sh
operator-sdk new podset-operator --type=go --skip-git-init
```

Navigate to the project root:

```sh
cd podset-operator
```

## Operator scope

A namespace-scoped operator (the default) watches and manages resources in a single namespace, whereas a cluster-scoped operator watches and manages resources cluster-wide. Namespace-scoped operators are preferred because of their flexibility. They enable decoupled upgrades, namespace isolation for failures and monitoring, and differing API definitions. However, there are use cases where a cluster-scoped operator may make sense. For example, the cert-manager operator is often deployed with cluster-scoped permissions and watches so that it can manage issuing certificates for an entire cluster.

If you'd like to create your memcached-operator project to be cluster-scoped use the following operator-sdk new command instead:

```sh
operator-sdk new podset-operator --cluster-scoped
```

## Project Scaffolding Layout

The operator-sdk CLI generates a number of packages for each project. The following table describes a basic rundown of each generated file/directory.

| File/Folders | Purpose |
| --- | --- |
| cmd | Contains manager/main.go which is the main program of the operator. This instantiates a new manager which registers all custom resource definitions under pkg/apis/... and starts all controllers under pkg/controllers/... . |
| pkg/apis | Contains the directory tree that defines the APIs of the Custom Resource Definitions(CRD). Users are expected to edit the pkg/apis/<group>/<version>/<kind>_types.go files to define the API for each resource type and import these packages in their controllers to watch for these resource types. |
| pkg/controller | This pkg contains the controller implementations. Users are expected to edit the pkg/controller/<kind>/<kind>_controller.go to define the controller's reconcile logic for handling a resource type of the specified kind. |
| build | Contains the Dockerfile and build scripts used to build the operator. |
| deploy | Contains various YAML manifests for registering CRDs, setting up RBAC, and deploying the operator as a Deployment. |
| Gopkg.toml Gopkg.lock | The Go Dep manifests that describe the external dependencies of this operator. |
| vendor | The golang vendor folder that contains the local copies of the external dependencies that satisfy the imports of this project. Go Dep manages the vendor directly. |
