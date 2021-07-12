Use:

`helm template hello-kubernetes . | less`{{execute}}

You should see all the resources that Helm will create (the same as the resource files we copied into `/templates`). Press `q` to exit from the view.

Finally let's install our basic chart `helm install [NAME] [FOLDER]`:

`helm install hello-kubernetes .`{{execute}}

Check details of the deployment:

`helm list`{{execute}}

Check all the resources deployed in Kubernetes:
`kubectl get all`{{execute}}

Wait until the pods status is `Running`.
`kubectl get pods`{{execute}}

Expose the application to verify it is running:
`POD=$(kubectl get pod -o jsonpath="{.items[0].metadata.name}")`{{execute}}
`kubectl port-forward $POD 8080:8080 --address 0.0.0.0`{{execute}}

Click the `Display 8080` tab in the terminal window. Notice how the image version is `1.10`. Press `Control + C` to stop forwarding.
