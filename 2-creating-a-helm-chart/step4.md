**Answer:** you can use `helm template` to render the files and see all the resources that Helm will create for us.

Go to the `cd /root/hello-kubernetes/deploy/resources/helm/hello-kubernetes/`{{execute}} directory and test that the chart can be rendered following `helm template [NAME] [FOLDER]`:

`helm template hello-kubernetes . | less`{{execute}}

`hello-kubernetes` is the name we want to give the application, `.` indicates to use the local directory. You should see all the resources that Helm will create (the same as the resource files we copied into `/templates` - services, deployment and serviceAccount). Press `q` to exit from the view.

### Install the hello-kubernetes application

Finally let's install our basic chart for the `hello-kubernetes` application using `helm install [NAME] [FOLDER]`:

`helm install hello-kubernetes .`{{execute}}

`hello-kubernetes` is the name we want to give the application so it can be tracked by Helm. Check details of the deployment:

`helm list`{{execute}}

Notice how the chart version and app version match the `version` and `appVersion` defined in the `Chart.yaml` file. 

### Verify application is deployed

Check all the resources are deployed in Kubernetes (serviceaccount, deployment, service and pod - created by the deployment) using `kubectl`:
`kubectl get all -l app.kubernetes.io/name=hello-kubernetes`{{execute}}

Use `kubectl` to see the pods starting. Wait until the pods status is `Running`.
`kubectl get pods`{{execute}}

Expose the application to verify it is running:
`POD=$(kubectl get pod -o jsonpath="{.items[0].metadata.name}")`{{execute}}
`kubectl port-forward $POD 8080:8080 --address 0.0.0.0`{{execute}}

Click the `Display 8080` tab in the terminal window. Notice how the image version is `1.10`. Press `Control + C` to stop forwarding.

### Question:

**What other Helm command can we run to verify the application deployment and obtain more information?**
