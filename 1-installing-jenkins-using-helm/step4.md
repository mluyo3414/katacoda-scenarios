**Answer**: `helm list` displays the applications installed using Helm.


### List applications installed with Helm

Run `helm list` again to see the deployed application (you can use `--all-namespaces` to see all applications installed using Helm in Kubernetes or `-n jenkins` to only look at our namespace) :

`helm list --all-namespaces`{{execute}}

Notice this installation `REVISION:1` (first time we install this chart), `CHART:jenkins-3.3.21` and `APPLICATION:2.277.4`. 

Any change in our configuration either by a new `values.yaml` file, an upgrade, or adding a new configuration parameter will increase our revision number.


### Upgrading Jenkins

Now, lets upgrade to the chart version `3.4.1` with the same values file (you can also execute `--dry-run` to test and `helm show values` to see new options):

`helm upgrade jenkins jenkins/jenkins -n jenkins --version 3.4.1 -f values.yaml`{{execute}}

Wait for the new pod to start running `kubectl get pods -n jenkins -w`{{execute}}. Press `Control + C` once pod is running.

Now double check that a new application was deployed:

`helm list --all-namespaces`{{execute}} should provide `REVISION:2`, `CHART:jenkins-3.4.1` and `APPLICATION:2.289.1`. 

![upgrade](./../assets/upgrade.png)


### Exposing upgraded applications

Run `kubectl port-forward jenkins-0 8080:8080 --address 0.0.0.0 -n jenkins`{{execute}} to expose the application. 

Open a new window again by clicking `Display 8080`, login user the same `admin` username and the same password as before (remember you can run `helm status jenkins -n jenkins`{{execute}} if you forgot your password or the command to get it). 

Once you access the UI, you should be able to see that the application version in the bottom right is `Jenkins 2.289.1` now. Exit the port-forward by pressing `Control+C` in the terminal.


### Verifying Kubernetes resources installed

As mentioned before, Helm offers a level of abstraction on top of K8s resources but you can run  `kubectl get all -n jenkins`{{execute}} and see all the Kubernetes resources deployed by Helm corresponding to the Jenkins application. 

