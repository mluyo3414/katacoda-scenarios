## Overview

In this tutorial, you will learn how to install a containerized version of [Jenkins](https://www.jenkins.io/) in [Kubernetes](https://kubernetes.io/) using [Helm](https://helm.sh/). 

* Kubernetes, also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications. Learn more about Kubernetes and its advantages in [this link](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/).

* Helm is the Kubernetes native package manager, it allows to install and manage applications in Kubernetes without the need to deploy multiple resource files. 

* Finally, Jenkins is a widely used automation tool that can leverage Kubernetes to deploy other containers (called [agents](https://www.jenkins.io/doc/book/using/using-agents/)) and run tasks in them (usually focused on building, testing and deploying other applications).


## [The purpose of Helm](https://helm.sh/docs/topics/architecture/)

Helm is a tool for managing Kubernetes packages called *charts*. Helm can do the following:

* Create new charts from scratch
* Package charts into chart archive (tgz) files
* *Interact with chart repositories where charts are stored (in this tutorial)*
* *Install and uninstall charts into an existing Kubernetes cluster (in this tutorial)*
* Manage the release cycle of charts that have been installed with Helm

For Helm, there are three important concepts:

* The chart is a bundle of information necessary to create an instance of a Kubernetes application.
* The config contains configuration information that can be merged into a packaged chart to create a releasable object.
* A release is a running instance of a chart, combined with a specific config.

In this scenario, we will learn:
* How to install and upgrade a [Jenkins controller](https://www.jenkins.io/doc/book/glossary/#general-terms) from its public [Helm chart](https://github.com/jenkinsci/helm-charts/tree/main/charts/jenkins).
* How to interact with the Helm client to obtain useful application information.


## Prerequisites

1. Familiarity with the terminal and have some previous experience with containers.

## Learning Objectives

1. Understand what Helm is and its role in Kubernetes.
2. Become familiar with the Helm client using the terminal.
3. Learn the necessary Helm client commands to inspect, install, and upgrade a Helm public chart.
4. Learn how to verify an application is installed when using Helm


![Helm Logo](./../assets/intro.png)

