# Overview

Fiddler app overview

# Installation

## Quick install with Google Cloud Marketplace

Get up and running with a few clicks! Install this Fiddler app to a Google
Kubernetes Engine cluster using Google Cloud Marketplace. Follow the on-screen instructions:

-----> *TODO*: link to product details page*

## Command line instructions

Follow these instructions to install Fiddler from the command line.

### Prerequisites

#### Set up command-line tools

----> *TODO*: to be compleleted

You'll need the following tools in your development environment. If you are
using Cloud Shell, `gcloud`, `kubectl`, Docker, and Git are installed in your
environment by default.

-   [gcloud](https://cloud.google.com/sdk/gcloud/)
-   [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)
-   [docker](https://docs.docker.com/install/)
-   [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
-   [openssl](https://www.openssl.org/)
-   [helm](https://helm.sh/)

Configure `gcloud` as a Docker credential helper:

```shell
gcloud auth configure-docker
```

#### Create a Google Kubernetes Engine (GKE) cluster

Create variables from the command line:

```shell
export CLUSTER=fiddler-prod-cluster
export ZONE=us-west1-a
```

Configure `kubectl` to connect to the new cluster:

```shell
gcloud container clusters get-credentials "$CLUSTER" --zone "$ZONE"
```

#### Clone this repo

```shell
git clone --recursive https://github.com/GoogleCloudPlatform/marketplace-k8s-app-example.git
```

#### Install the Application resource definition

An Application resource is a collection of individual Kubernetes components,
such as Services, Deployments, and so on, that you can manage as a group.

To set up your cluster to understand Application resources, run the following
command:

```shell
kubectl apply -f "https://raw.githubusercontent.com/GoogleCloudPlatform/marketplace-k8s-app-tools/master/crd/app-crd.yaml"
```

You need to run this command once.

The Application resource is defined by the
[Kubernetes SIG-apps](https://github.com/kubernetes/community/tree/master/sig-apps)
community. The source code can be found on
[github.com/kubernetes-sigs/application](https://github.com/kubernetes-sigs/application).

### Install the application

### Commands

*TODO: Modify commands*


# Backups

*TODO: instructions for backups*

# Upgrades

*TODO: instructions for upgrades*