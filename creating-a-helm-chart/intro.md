In this tutorial, we will learn how to create a Helm chart to maintain an example application - https://github.com/mluyo3414/hello-kubernetes (credit to paulbouwer who created it). 

* [Kubernetes](https://kubernetes.io/), also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications. 

* [Helm](https://helm.sh/) is the Kubernetes native package manager, it allows to install and manage applications in Kubernetes without the need to deploy multiple resource files (YAML files). 

* A [Helm Chart](https://helm.sh/docs/topics/charts/) is a collection of files that describe a related set of Kubernetes resources.

The example application consists on a [service account](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/), a [deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) and a [service](https://kubernetes.io/docs/concepts/services-networking/service/) which are already created.
