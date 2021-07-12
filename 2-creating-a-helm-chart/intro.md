## Overview


In this tutorial, we will learn how to create a Helm chart to maintain an example application - https://github.com/mluyo3414/hello-kubernetes (credit to paulbouwer who created it). 

## Technologies review

* [Kubernetes](https://kubernetes.io/), also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications. 

* [Helm](https://helm.sh/) is the Kubernetes native package manager, it allows to install and manage applications in Kubernetes without the need to deploy multiple resource files (YAML files). 

* A [Helm Chart](https://helm.sh/docs/topics/charts/) is a collection of files that describe a related set of Kubernetes resources.

## Application


The example application consists on a [service account](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/), a [deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) and a [service](https://kubernetes.io/docs/concepts/services-networking/service/) which are already created.


## Prerequisites

1. Familiarity with the terminal and have some previous experience with containers.
2. Complete [part 1 of this Helm tutorial](https://katacoda.com/msuarez/scenarios/1-installing-jenkins-using-helm)

## Learning Objectives

1. Understand some of the basic components needed to deploy an application in Kubernetes.
2. Learn how to create a basic Helm chart using those files.
3. Learn how to add variables to a Helm chart.
