Answer: `helm list` displays the applications installed using Helm.


### List applications installed with Helm

Run helm list again to see the deployed application:

`helm list --all-namespaces`{{execute}}

Notice this installation `REVISION:1` (first time we install this chart), `CHART:jenkins-3.3.21` and `APPLICATION:2.277.4`. 


### Upgrading Jenkins

Now, lets upgrade to the version `3.4.1` with the same parameters (you can also execute `--dry-run` to test and `helm show values` to see new options):

`helm upgrade jenkins jenkins/jenkins -n jenkins --version 3.4.1 -f values.yaml`{{execute}}

Wait for the new pod to start running `kubectl get pods -n jenkins -w`{{execute}}. `Control + C` once pod is running.

Now double check that a new application was deployed:

`helm list --all-namespaces`{{execute}} should provide `REVISION:2`, `CHART:jenkins-3.4.1` and `APPLICATION:2.289.1`. 

![upgrade](./../assets/upgrade.png)


### Exposing upgraded applications

Run `kubectl port-forward jenkins-0 8080:8080 --address 0.0.0.0 -n jenkins`{{execute}} to expose the application. 
Open a new window again by clicking `Display 8080`, login user the same `admin` username and the same password as before. 

You should be able to see that the application version in the bottom right is `Jenkins 2.289.1` now. Exit the port-forward by pressing `Control+C` in the terminal.


### Verifying Kubernetes resources installed

You can run  `kubectl get all -n jenkins`{{execute}} and see all the Kubernetes resources deployed by Helm. 

