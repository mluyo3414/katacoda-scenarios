**Answer:** Running `helm status hello-kubernetes`{{execute}} can provide more information.

### Defining new variables for the application

As we mentioned before in both tutorials, Helm provides the option to add different options to configure the installation of an application. 

Let's define which variables can be set in our `hello-kubernetes` chart to make it easier to deploy it in different environments or just make it easier to manage. To be more specific, we are going to define the variables we can pass values for using `--set` or `-f values.yaml` when we use `helm upgrade` or `helm install`. 

**Our goal in this case will be to convert the hardcoded Docker image value for our application to a variable so we can select which application image we want to use when using Helm. In this specific example we will upgrade from the image already installed (tagged `1.10`) to the image tagged as `1.11-dev`.**

* First, go to the `Chart.yaml` and change the `appVersion` to `1.11`. This file is not using a variable and it is not mandatory to change but it is the value shown when we use `helm list`. Since we are going to be upgrading the image in the  `deployment`, it is recommended to upgrade the `appVersion` field as well to match the image.

* Go to `values.yaml`, **delete everything** and insert:

```
deployment:
  image: "mluyo3414/hello-kubernetes"
  tag: "1.11-dev"
```{{copy}}

* Go to the `image` section (around line 23) in the `deployment.yaml` and change:

```
image: "mluyo3414/hello-kubernetes:1.10"
```

to:

```
image: {{  .Values.deployment.image  }}:{{  .Values.deployment.tag  }}
```{{copy}}

* Also, go to the `value` section under CONTAINER_IMAGE (around line 51) in the `deployment.yaml` and change from:

```
value: "mluyo3414/hello-kubernetes:1.10"
```

to:

```
value: {{  .Values.deployment.image  }}:{{  .Values.deployment.tag  }}
```{{copy}}

Helm uses Go templating to insert variables. As you can see, the variables follow the format used in `values.yaml`.


### Using the Chart variable


Let's upgrade our already installed application to the new version `1.11-dev` using our new variable.

Make sure you are inside the correct folder first and then upgrade:

`cd /root/hello-kubernetes/deploy/resources/helm/hello-kubernetes/`{{execute}}

`helm upgrade hello-kubernetes . --values values.yaml`{{execute}}

### Verify the new version in the application and expose it

Check the details of the deployment:

`helm list`{{execute}}

You should now see `REVISION:2`

Check all the application resources are deployed in Kubernetes and make sure the corresponding pods are `Running`:

`kubectl get all -l app.kubernetes.io/name=hello-kubernetes`{{execute}}

All deployed resources for the app have the `hello-kubernetes` value for the `app.kubernetes.io/name` label. You can find the labels in the [YAML files](https://github.com/mluyo3414/hello-kubernetes/blob/main/deploy/resources/service.yaml#L6). Labels are used to group resources easily.

Get the pod name and expose the application to verify it is running:

`POD=$(kubectl get pod -o jsonpath="{.items[0].metadata.name}")`{{execute}}

`kubectl port-forward $POD 8080:8080 --address 0.0.0.0`{{execute}}

Click the `Display 8080` tab in the terminal window. **Notice how the image version is `1.11-dev`. Press `Control + C` to stop forwarding.**

This is a simple application but Helm provides easier management for complicated applications that can be composed of several resources without the need to keep track of multiple YAML files.

### Try creating a new variable yourself:

Look at the `metadata.name` field in the `deployment.yaml` or `service.yaml` we are using for our chart. Notice how the value for this field is the same string `hello-kubernetes-hello-kubernetes`. How would you templatize it so it can be assigned in `values.yaml`?



