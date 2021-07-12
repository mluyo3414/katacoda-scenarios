Let's insert some variables in our chart to make it easier to deploy it in different environments. We will start by changing the image version to `1.11`.

* Go to the Chart.yaml and change the appVersion to `1.11`

* Go to `values.yaml`, **delete everything** and insert:

```
deployment:
  image: "mluyo3414/hello-kubernetes"
  tag: "1.11"
```{{copy}}

* Go to the `image` section (around line 23) in the `deployment.yaml` from:

```
image: "mluyo3414/hello-kubernetes:1.10"
```

to:

```
image: {{  .Values.deployment.image  }}:{{  .Values.deployment.tag  }}
```{{copy}}

* Also, go to the `value` section under CONTAINER_IMAGE (around line 51) in the `deployment.yaml` from:

```
value: "mluyo3414/hello-kubernetes:1.10"
```

to:

```
value: {{  .Values.deployment.image  }}:{{  .Values.deployment.tag  }}
```{{copy}}

Helm uses Go templating to insert variables. Let's upgrade our already installed application to the new version `1.11` (make sure you are inside the correct folder `cd /root/hello-kubernetes/deploy/resources/helm/hello-kubernetes/`{{execute}}):

`helm upgrade hello-kubernetes . --values values.yaml`{{execute}}

Check details of the deployment:

`helm list`{{execute}}

Check all the resources deployed in Kubernetes:
`kubectl get all`{{execute}}

Expose the application to verify it is running:
`POD=$(kubectl get pod -o jsonpath="{.items[0].metadata.name}")`{{execute}}
`kubectl port-forward $POD 8080:8080 --address 0.0.0.0`{{execute}}

Click the `Display 8080` tab in the terminal window. Notice how the image version is `1.11`. Press `Control + C` to stop forwarding.

**Please take this [quiz](https://forms.gle/fEPAdta7CAA1JGgY8) to validate your knowledge after the tutorials. Also, please provide me [feedback](https://forms.gle/4UcbcuAVBXmDGdtQ9to) to improve these tutorials.**


