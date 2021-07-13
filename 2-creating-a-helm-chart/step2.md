
**Answer**: You can use `helm list` to see any applications installed in any namespace:

`helm list --all-namespaces`{{execute}}

### Understanding the Hello-Kubernetes Application

Now, let's start by cloning the application:

`git clone https://github.com/mluyo3414/hello-kubernetes.git`{{execute}}

You can see the application in the top folder of the VSCode window on the top right. The application code and `Dockerfile` are located under `/src/app`.

There are **four** files that represent the resources needed to deploy the application in Kubernetes. They are located under **`hello-kubernetes/deploy/resources`** (**`all-resources.yaml`** is a single file that includes all resources):

* `serviceaccount.yaml` : A service account provides an identity for processes that run in a Pod. 

* `deployment.yaml` : A Deployment provides declarative updates for [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) and [ReplicaSets](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

* `service.yaml` : An abstract way to expose an application running on a set of Pods as a network service.

* `all-resources.yaml` : an example about how to have all the files togeher in a single file so the application can be installed with `kubectl apply -f resources.yaml`

### Creating the hello-kubernetes chart

Now, let's make a directory inside the `resources` folder to create the [Helm chart](https://helm.sh/docs/topics/charts/) and package the application:

`mkdir hello-kubernetes/deploy/resources/helm && cd $_`{{execute}}

Create the `hello-kubernetes` chart:

`helm create hello-kubernetes`{{execute}}

Helm has now created a Chart inside `hello-kubernetes/deploy/resources/helm` under `hello-kubernetes`. [This link](https://helm.sh/docs/topics/charts/#the-chart-file-structure) contains all the information about what each file. The most important files/directories are:

* **`Chart.yaml`**: Chart name, description, version and information about the chart.

* **`values.yaml`**: File where we can define/overwrite variables for the Chart: things like image tag, persistent volumes, etc. This specific file in our repo will contain the default values but it can be replaced by other `values.yaml` when we want to install the application somewhere else.

* **`templates/`**: All Kubernetes YAML files we would like to include in the Chart.

### Question:

**Which files do you think you need to include under `templates/` folder to create a chart for the `hello-kubernetes` application?**

Click *Continue* to see the response in the next screen.



