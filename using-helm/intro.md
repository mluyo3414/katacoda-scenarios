In this tutorial, you will learn how to install a containerized version of Jenkins in Kubernetes using Helm. Kubernetes, also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications. Helm is the Kubernetes native package manager, it allows to install and manage applications in Kubernetes without the need to deploy multiple resource files (YAML files). Finally, Jenkins is a widely used automation tool that can leverage containerization in Kubernetes to deploy containers (called agents) and run tasks usually focused on building, testing and deploying applications.

In this first scenario, we will learn:
* How to install and upgrade [Jenkins](https://www.jenkins.io/) from its public [Helm chart](https://github.com/jenkinsci/helm-charts/tree/main/charts/jenkins).
* How to interact with the Helm client to obtain useful application information.

![Helm Logo](./../assets/intro.png)
