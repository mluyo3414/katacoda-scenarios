**Answer:** Running `helm status hello-kubernetes`{{execute}} can provide more information.

### Defining variables for the application

As we mentioned before in both tutorials, Helm provides the option to add different options to configure the installation of an application. 

Let's define which variables can be set in our `hello-kubernetes` chart to make it easier to deploy it in different environments or share it with other users (we are going to define the variables we can pass values for using `--set` or `-f values.yaml`). 

**In this case, we will convert the Docker image value for our application to a variable so we can select which application image we want to install.**

Our goal is to now upgrade from the image tagged `1.10` to the `1.11-dev`

* First, go to the `Chart.yaml` and change the `appVersion` to `1.11`. This is not a variable but it is the value shown when we use `helm list` and since we are going to be upgrading the image in the   `deployment` it is recommended to upgrade this chart field as well.

* Go to `values.yaml`, **delete everything** and insert:

```
deployment:
  image: "mluyo3414/hello-kubernetes"
  tag: "1.11-dev"
```{{copy}}

* Now let's use templating to create a variable. Go to the `image` section (around line 23) in the `deployment.yaml` and change:

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

Helm uses Go templating to insert variables. Let's upgrade our already installed application to the new version `1.11-dev` 

Make sure you are inside the correct folder first and then upgrade:
`cd /root/hello-kubernetes/deploy/resources/helm/hello-kubernetes/`{{execute}}):

`helm upgrade hello-kubernetes . --values values.yaml`{{execute}}

### Verify the new version in the application

Check details of the deployment:

`helm list`{{execute}}

You should now see `REVISION:2`

Check all the resources deployed in Kubernetes:
`kubectl get all`{{execute}}

Expose the application to verify it is running:
`POD=$(kubectl get pod -o jsonpath="{.items[0].metadata.name}")`{{execute}}
`kubectl port-forward $POD 8080:8080 --address 0.0.0.0`{{execute}}

Click the `Display 8080` tab in the terminal window. **Notice how the image version is `1.11-dev`. Press `Control + C` to stop forwarding.**

This is a simple application but Helm provides easier management for complicated applications that can be composed of several resources without the need to keep track of multiple YAML files.

### Try creating a new variable yourself:

Look at the `metadata.name` field in the `deployment.yaml` or `service.yaml` we are using for our chart. Notice how the value for this field is the same string `hello-kubernetes-hello-kubernetes`. How would you templatize it so it can be assigned in `values.yaml`?



