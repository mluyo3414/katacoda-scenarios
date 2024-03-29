## Scenario Overview


In this part, we will learn how to create a new Helm chart to maintain an example web application - https://github.com/mluyo3414/hello-kubernetes (credit to paulbouwer who created it). This is a continuation of [Helm tutorial part 1: Learning Helm by installing Jenkins](https://katacoda.com/msuarez/scenarios/1-installing-jenkins-using-helm).


## Technologies review 


* [Kubernetes](https://kubernetes.io/), also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications. 

* [Helm](https://helm.sh/) is the Kubernetes native package manager, it allows to install and manage applications in Kubernetes without the need to deploy multiple resource files (YAML files). 

* A [Helm Chart](https://helm.sh/docs/topics/charts/) is a collection of files that describe a related set of Kubernetes resources.


## Prerequisites


1. Familiarity with the terminal and have some previous experience with containers.
2. Complete [part 1 of this Helm tutorial](https://katacoda.com/msuarez/scenarios/1-installing-jenkins-using-helm)


## Learning Objectives

At the end of this scenario, you should:

1. Know some of the basic resources needed to deploy an application in Kubernetes.
2. Know how to create a basic Helm chart using the files belonging to those Kubernetes resources.
3. Know how to add variables to a Helm chart.
