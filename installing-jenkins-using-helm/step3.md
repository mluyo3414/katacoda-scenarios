Now let's install Jenkins with the `values.yaml` file:

`helm install jenkins jenkins/jenkins -n jenkins --version 3.4.0 -f values.yaml`{{execute}}

Also, you can see if the pod is running:

`kubectl get pods -n jenkins -w`{{execute}}

Press `Control+C` to exit once the pod `Status` is `Running`.

You can see the status and useful information of the Helm deployment (the same message that you just when you executed `helm install ..`) by running:

`helm status jenkins -n jenkins`{{execute}}

Copy the command to get your console password (Step 1 in the Helm status message):

`kubectl exec --namespace jenkins -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/chart-admin-password && echo`{{execute}}

Now, `port-forward` the console so you can see it in your browser (the command is a bit different for our environment than the one provided by Helm status):

`kubectl port-forward jenkins-0 8080:8080 --address 0.0.0.0 -n jenkins`{{execute}}

Click on `Display 8080` in the terminal options so it opens a new window:

![Helm Logo](./../assets/8080.png)

Login with the user **admin** and the password you retrieved.




