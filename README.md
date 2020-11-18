# Kubernetes Flux Testing Repo

A FluxCD configuration for a demo cluster running on AKS.

## Prerequisites

### Azure CLI Prerequisites

As part of this demo, make sure all of the preview extensions are up to date.

```bash
az extension add --name connectedk8s
az extension add --name k8sconfiguration

az extension update --name aks-preview
az extension update --name connectedk8s
az extension update --name k8sconfiguration
```

### Setup Shell Variables

These variables will be used throughout the demo.

```bash
NAME=cdw-apimgmt-20201113

# Azure Arc is limited to East US (among a few others), so use it
LOCATION=eastus
```

## Azure Resource Setup

### Create an Azure Resource Group

```bash
az group create -n $NAME -l $LOCATION
```

### Create an Azure Kubernetes Cluster

```bash
# Create cluster
az aks create \
--resource-group $NAME \
--name $NAME \
--location $LOCATION \
--kubernetes-version 1.18.10 \
--generate-ssh-keys \
--enable-managed-identity

# --enable-addons monitoring

az aks get-credentials -n $NAME -g $NAME --overwrite

# Delete cluster
az aks delete \
--resource-group $NAME \
--name $NAME
```

## Configuration Setup

* [API Management](/bases/apim-gateway/README.md)

* [Azure Service Operator](/bases/operators/azure/README.md)

## Setup Cluster for Azure Arc

### Add Cluster to Azure Arc

```bash
az connectedk8s connect --resource-group $NAME --name $NAME --location $LOCATION
```

### Add FluxCD to Arc-enabled Cluster

Azure Arc enables quick and easy configuration of FluxCD on your cluster.

```bash
# Create the Flux config with the CLI
az k8sconfiguration create \
--name flux-cluster-01 \
--cluster-name $NAME \
--resource-group $NAME \
--scope cluster \
--cluster-type connectedClusters \
--operator-namespace flux-cluster-01 \
--operator-instance-name flux \
--operator-params '--git-readonly --git-branch master --git-path production --manifest-generation=true --git-poll-interval=3m' \
--repository-url https://github.com/cwiederspan/aks-flux-cluster01.git \
--enable-helm-operator \
--helm-operator-version='1.2.0' \
--helm-operator-params='--set helm.versions=v3'

# Delete the Flux config with the CLI
az k8sconfiguration delete \
--name flux-cluster-01 \
--cluster-name $NAME \
--cluster-type connectedClusters \
--resource-group $NAME
```
