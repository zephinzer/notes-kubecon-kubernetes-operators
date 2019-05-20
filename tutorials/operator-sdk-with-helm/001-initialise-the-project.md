# Initialize the Project

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

Create a new Helm-based Operator SDK project for the CockroachDB Operator:

```sh
operator-sdk new cockroachdb-operator --type=helm --helm-chart cockroachdb --helm-chart-repo https://kubernetes-charts.storage.googleapis.com
```

Navigate to the top-level project directory:

```sh
cd cockroachdb-operator
```

## Project Scaffolding Layout

After creating a new operator project using operator-sdk new --type helm, the project directory has numerous generated folders and files. The following table describes a basic rundown of the generated files and directories:

| File/Folders | Purpose |
| --- | --- |
| deploy | Contains a generic set of Kubernetes manifests for deploying this operator on a Kubernetes cluster. |
| helm-charts/ | Contains a Helm chart initialized using the equivalent of [helm create][docs_helm_create] |
| build | Contains scripts that the operator-sdk uses for build and initialization. |
| watches.yaml | Contains Group, Version, Kind, and Helm chart location. |
