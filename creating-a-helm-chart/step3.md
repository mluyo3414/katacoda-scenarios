Start by cloning the application:

`git clone https://github.com/mluyo3414/hello-kubernetes.git`{{execute}}

Now you can see the application in the top folder of the VSCode window on the top right.

There are **four** files inside `deploy/resources`. `serviceaccount.yaml`, `deployment.yaml`, and `service.yaml` compose the pplication (`all-resources.yaml` is a single file that includes all resources)  :

* `serviceaccount.yaml` : A service account provides an identity for processes that run in a Pod. 

* `deployment.yaml` : A Deployment provides declarative updates for [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) and [ReplicaSets](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

* `service.yaml` : An abstract way to expose an application running on a set of Pods as a network service.

* `all-resources.yaml` : an example about how to have all the files togeher in a single file so the application can be installed with `kubectl apply -f resources.yaml`


