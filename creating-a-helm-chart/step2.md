Start by cloning the application:

`git clone https://github.com/mluyo3414/hello-kubernetes.git`{{execute}}

Now you can see the application in the top folder of the VSCode window on the top right.

There are **four** files inside **`hello-kubernetes/deploy/resources`**. **`serviceaccount.yaml`**, **`deployment.yaml`**, and **`service.yaml`** that compose the pplication (**`all-resources.yaml`** is a single file that includes all resources)  :

* `serviceaccount.yaml` : A service account provides an identity for processes that run in a Pod. 

* `deployment.yaml` : A Deployment provides declarative updates for [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) and [ReplicaSets](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

* `service.yaml` : An abstract way to expose an application running on a set of Pods as a network service.

* `all-resources.yaml` : an example about how to have all the files togeher in a single file so the application can be installed with `kubectl apply -f resources.yaml`

Now, let's make a directory inside the `resources` folder to create the [Helm chart](https://helm.sh/docs/topics/charts/) and package the application:

`mkdir hello-kubernetes/deploy/resources/helm && cd $_`{{execute}}

Create the `hello-kubernetes` chart:

`helm create hello-kubernetes`{{execute}}

Helm has now created a Chart inside `hello-kubernetes/deploy/resources/helm` under `hello-kubernetes`. [This link](https://helm.sh/docs/topics/charts/#the-chart-file-structure) contains all the information about what each file. The most important files/directories are:

* **`Chart.yaml`**: Chart name, description, version and information about the chart.

* **`values.yaml`**: File where we can define/overwrite variables for the Chart: things like image tag, persistent volumes, etc. This specific file in our repo will contain the default values but it can be replaced by other `values.yaml` when we want to install the application somewhere else.

* **`templates/`**: All YAML files we would like to include in the Chart (`service.yaml`, `serviceaccount.yaml`, and `deployment.yaml` in our case for the `hello-kubernetes` application).

Let's cleanup the template and add our application YAML files.

* Delete the **`templates/tests`** folder inside :

* Delete everything on **`templates`** besides **`_helpers.tpl`** file:

* Move the **`serviceaccount.yaml`**, **`deployment.yaml`**, and **`service.yaml`** into the **`templates/`** directory to be used by the Chart.


This is how the final configuration under `/root/hello-kubernetes/deploy/resources` should look like:
```
├── all-resources.yaml
└── helm
    └── hello-kubernetes
        ├── charts
        ├── Chart.yaml
        ├── templates
        │   ├── deployment.yaml
        │   ├── _helpers.tpl
        │   ├── serviceaccount.yaml
        │   └── service.yaml
        └── values.yaml
```

* Inspect the `Chart.yaml` file. Notice how there is a `version` for the chart version and a `appVersion` for the application version itself.

Go to the `cd /root/hello-kubernetes/deploy/resources/helm/hello-kubernetes/`{{execute}} directory and test that the chart can be rendered `helm template [NAME] [FOLDER]`:

`helm template hello-kubernetes . | less`{{execute}}

You should see all the resources that Helm will create (the same as the resource files we copied into `/templates`). Press `q` to exit from the view.

Finally let's install our basic chart `helm install [NAME] [FOLDER]`:

`helm install hello-kubernetes .`{{execute}}

Check details of the deployment:

`helm list`{{execute}}

Check all the resources deployed in Kubernetes:
`kubectl get all`{{execute}}

Expose the application to verify it is running:
`POD=$(kubectl get pod -o jsonpath="{.items[0].metadata.name}")`{{execute}}
`kubectl port-forward $POD 8080:8080 --address 0.0.0.0`{{execute}}

Click the `Display 8080` tab in the terminal window. Notice how the image version is `1.10`



