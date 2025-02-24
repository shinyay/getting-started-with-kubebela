# Getting Started with KubeVela with AKS

KubeVela is a modern application delivery platform designed to make deploying and operating applications across hybrid and multi-cloud environments easier, faster, and more reliable.
And KubeVela is built on top of Kubernetes and provides a set of abstractions and tools that simplify the process of deploying, managing, and scaling applications.

## Main Benefits of KubeVela
- Simplifies application deployment across different environments
- Provides consistent delivery experience
- Supports hybrid and multi-cloud deployments
- Makes application operations more reliable
- Offers extensible and programmable workflows

## Description

### 1. Core Features

- **Infrastructure agnostic**: Works across different cloud providers and environments
- **Application-centric**: Focuses on application delivery rather than infrastructure management
- **Programmable**: Allows customization and automation of delivery workflows
- **Built on Kubernetes**: Leverages Kubernetes as its control plane
- **Open Application Model (OAM) based**: Uses OAM for application definition and orchestration

### 2. Open Application Model (OAM)\
OAM is a specification for defining and deploying applications in a cloud-native environment. It provides a set of abstractions and APIs that allow developers to describe their applications in a way that is independent of the underlying infrastructure.
OAM defines three main concepts:
- **Components**: The building blocks of an application, such as microservices, databases, and message queues.
- **Traits**: Additional functionality that can be applied to components, such as scaling, monitoring, and logging.
- **Scopes**: The environment in which the application is deployed, such as a Kubernetes cluster or a cloud provider.

## Demo

### 1. Create an AKS Cluster

```fish
# Login to Azure
az login

# Create a resource group
az group create --name shinyayRG --location eastus

# Create an AKS cluster
az aks create \
    --resource-group shinyayRG \
    --name shinyayAKS \
    --node-count 3 \
    --enable-addons monitoring \
    --generate-ssh-keys

# Get the AKS cluster credentials
az aks get-credentials --resource-group shinyayRG --name shinyayAKS
```

### 2. Install KubeVela (Using Helm)
KubeVela can be installed using Helm, a package manager for Kubernetes. Helm allows you to easily install and manage applications on Kubernetes.

```fish
# Add the KubeVela Helm repository
helm repo add kubevela https://charts.kubevela.net/core

# Update the Helm repository
helm repo update

# Install KubeVela using Helm
helm install kubevela kubevela/vela-core \
    --namespace vela-system \
    --create-namespace \
    --set global.clusterLocal=true \
    --set global.enableHelm=true \
    --set global.enableOCI=true \
    --set global.enableLogging=true \
    --set global.enableMonitoring=true

# Verify the installation
kubectl get pods -n vela-system
```

<details>
<summary>Click to see the output of the above command</summary>

```text
NAME: kubevela
LAST DEPLOYED: Mon Feb 24 22:45:04 2025
NAMESPACE: vela-system
STATUS: deployed
REVISION: 1
NOTES:
Welcome to use the KubeVela! Enjoy your shipping application journey!

                                   ,
                                   //,
                                   ////
                               ./  /////*
                             ,///  ///////
                           ./////  ////////
                          ///////  /////////
                         ////////  //////////
                       ,/////////  ///////////
                      ,//////////  ///////////.
                     .///////////  ////////////
                     ////////////  ////////////.
                    *////////////  ////////////*
       #@@@@@@@@@@@*     ..,,***/  /////////////
        /@@@@@@@@@@@#
         *@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@&
          .@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@.

              @@@@@@@@@@@@@@@@@@@@@@@@@@@@@
                .&@@@*    *@@@&    ,@@@&.

       _  __       _          __     __     _
      | |/ /_   _ | |__    ___\ \   / /___ | |  __ _
      | ' /| | | || '_ \  / _ \\ \ / // _ \| | / _` |
      | . \| |_| || |_) ||  __/ \ V /|  __/| || (_| |
      |_|\_\\__,_||_.__/  \___|  \_/  \___||_| \__,_|


You can refer to https://kubevela.io for more details.
```
</details>

### 2. Install KubeVela (Using the KubeVela CLI)
KubeVela CLI is a command-line tool that provides a set of commands for managing KubeVela applications. It allows you to create, deploy, and manage applications using the OAM model.

```fish
# Install KubeVela CLI
curl -sL https://kubevela.io/script/install.sh | bash

# Verify the installation
vela version

# Install KubeVela on AKS
vela install \
    --namespace vela-system \
    --cluster-local \
    --enable-helm \
    --enable-oci \
    --enable-logging \
    --enable-monitoring

# Verify the installation
kubectl get pods -n vela-system
```

### 3. Create your first application

```yaml
# first-app.yaml
apiVersion: core.oam.dev/v1beta1
kind: Application
metadata:
  name: first-vela-app
  namespace: default

spec:
  components:
    - name: hello-world
      type: webservice
      properties:
        image: nginx
        ports:
          - port: 80
            expose: true
```

## Features

- feature:1
- feature:2

## Requirement

## Usage

## Installation

## References

## Licence

Released under the [MIT license](https://gist.githubusercontent.com/shinyay/56e54ee4c0e22db8211e05e70a63247e/raw/f3ac65a05ed8c8ea70b653875ccac0c6dbc10ba1/LICENSE)

## Author

- github: <https://github.com/shinyay>
- twitter: <https://twitter.com/yanashin18618>
- mastodon: <https://mastodon.social/@yanashin>
