## Scenario Overview

In this part, you will learn how to install a containerized version of [Jenkins](https://www.jenkins.io/) in [Kubernetes](https://kubernetes.io/) using [Helm](https://helm.sh/). Especifically, we will install and upgrade a [Jenkins controller](https://www.jenkins.io/doc/book/glossary/#general-terms) from its public [Helm chart](https://github.com/jenkinsci/helm-charts/tree/main/charts/jenkins). 


## Technologies 

1. Kubernetes, also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications. Learn more about Kubernetes and its advantages in [this link](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/).

2. Helm is the Kubernetes native package manager. It allows to install and manage applications in Kubernetes without the need to manage and configure multiple resource files in YAML. 

3. Finally, Jenkins (the application we will be installing with Helm) is a widely used automation tool that can leverage Kubernetes to deploy other containers (called [agents](https://www.jenkins.io/doc/book/using/using-agents/)) and run tasks in them (usually focused on building, testing and deploying other applications).

Jenkins when deployed in Kubernetes is composed of different parts (or resources) such as:

**[StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)** - manages the deployment and scaling of a set of Pods (a pod is the smallest deployable unit of computing that you can create and manage in Kubernetes. A pod contains one or more containers).

**[Service](https://kubernetes.io/docs/concepts/services-networking/service/)** - An abstract way to expose an application running on a set of Pods as a network service. This will allows us to access Jenkins.

## Why do we need Helm?

**Usually applications in K8s are composed of deployments, services, secrets, persistent volumes, etc. These are configured using one or multiple YAML files ([i.e deploying mySQL without Helm](https://kubernetes.io/docs/tasks/run-application/run-single-instance-stateful-application/)).** 

**Managing applications using YAML files can be complicated, that is why one of Helm's primary objectives is to provide a level of abstraction on top of these resources to facilitate the application lifecycle (installation, deployment in multiple environments, upgrade, rollback, etc). In our case, we will manage Jenkins and its k8s components (statefulSet and service) with Helm.** 


## [Overall usage of Helm](https://helm.sh/docs/topics/architecture/)

Helm manages applications using **charts** which are bundles of information necessary to create an instance of a Kubernetes application. Helm can do the following:

* **Interact with chart repositories where charts are stored (in this scenario - Part 1)**
* **Install and uninstall charts into an existing Kubernetes cluster (in this scenario - Part 1)**
* **Manage the release cycle (upgrade/rollback) of charts  that have been installed with Helm (in this scenario - Part 1)**
* Create new charts for applications from scratch (next scenario - Part 2)


## Prerequisites

1. Familiarity with the terminal and have some previous experience/knowledge with containers.

## Learning Objectives

At the end of this scenario, you should:

1. Understand what Helm is and its role in Kubernetes.
2. Be familiar with the Helm client using the terminal and obtain useful application information.
3. Know the necessary Helm client commands to inspect, install, and upgrade a Helm public chart.
4. Know how to verify an application is installed when using Helm.
5. Know and verify all k8s resources installed that are part of Jenkins.


![Helm Logo](./../assets/intro.png)

