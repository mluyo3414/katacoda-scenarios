The correct command to install an application is:

`helm install `

We are going to set the **application storage** to **false** since our ephemeral working environment does not offer a persistent volume and it will cause an error in our deployment. In order to do that, we need to change the `persistent` option to `false`. You can locate this option  **in or around line 707** in `values.yaml`:

```
persistence:
  enabled: true
```

There are two ways we can customize the installation of the Jenkins chart with this option. 

One option is to pass different values in the command line (we are going to also execute the `--dry-run` as we are not installing yet):

`helm install jenkins jenkins/jenkins -n jenkins --version 3.3.21 --set persistence.enabled=false --dry-run`{{execute}}

Another option is to pass the `values.yaml` file with the desired options (this is usually the preferred method as the file can be saved in version control). Go to the `values.yaml` file we created in VSCode, delete everything the persistence options we want to change (**Yes, delete the rest** - Helm will only change the persistent option to false and deploy all the rest of **default** options):

```
persistence:
  enabled: false
```{{copy}}

![Helm Logo](./../assets/values.png)

Now let's run the command (still with `--dry-run` as we are not installing yet!):

`helm install jenkins jenkins/jenkins -n jenkins --version 3.3.21 -f values.yaml --dry-run | less`{{execute}}

**Did you notice how you were able to see all the resources that were going to be created in your Kubernetes cluster when you added the `--dry-run` command (pod, secret, ConfigMap, etc)?**

An easier way to see the actual resources is to use `helm template`. This command can give you one file with all the resources needed to install the application. This is useful in cases where the Helm client is no available in the machine that is connected to your Kubernetes cluster and you can just run `kubectl apply -f $file_created_by_helm_template` :

`helm template jenkins jenkins/jenkins -n jenkins --version 3.3.21 -f values.yaml --dry-run > resources.yaml`{{execute}}

Take a look at the `resources.yaml` file in VSCode and see all the resources that Helm will install for you.

Now let's install Jenkins with the `values.yaml` file:

`helm install jenkins jenkins/jenkins -n jenkins --version 3.3.21 -f values.yaml`{{execute}}

Also, you can see if the pod is running:

`kubectl get pods -n jenkins -w`{{execute}} (`-w` to follow but it is optional)

Press `Control+C` to exit once the pod `Status` is `Running`. It should take a few minutes. 

You can see the status and useful information about the Helm deployment (the same message that you just when you executed `helm install ...`) by running:

`helm status jenkins -n jenkins`{{execute}}

Copy the command to get your console password (Step 1 in the Helm status message):

`kubectl exec --namespace jenkins -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/chart-admin-password && echo`{{execute}}

Now, `port-forward` the console so you can see it in your browser (the command is a bit different for our environment than the one provided by Helm status):

`kubectl port-forward jenkins-0 8080:8080 --address 0.0.0.0 -n jenkins`{{execute}}

Click on `Display 8080` in the terminal options so it opens a new window:

![8080](./../assets/8080.png)

Login with the user **admin** and the password you retrieved. Notice in the bottom right that the application version is `Jenkins 2.277.4`. 

Go back to the terminal window and press `Control+C` to stop forwarding. 

What command do you think you can use to see all the applications installed using Helm?

Click on `Continue` to see the correct answer.