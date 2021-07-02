Before we start, wait until Kubernetes has finished installing in the terminal window in the bottom right. You can also see what the content of the local environment is on the VSCode window on the top right. 

Start by verifying that the **Helm client** is installed.

* The Helm client can be installed in [different ways](https://helm.sh/docs/intro/install/) but in this case it has been already installed in our environment.

`helm version --short`{{execute}}


Check a few of the commands available:

`helm -h`{{execute}}


Verify there are no other applications installed in any namespace:

`helm list --all-namespaces`{{execute}}