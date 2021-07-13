
### Waiting for local environment

Before we start, wait until Kubernetes has finished installing in the terminal window in the bottom right. 

You can also see what the content of the local environment is on the VSCode window on the top right (if VSCode does not show up keep refreshing the browser until it shows "Loading VS Code - Please wait for the IDE to become available, this should only take a few seconds" and then "Connected"). 

### Verify Helm is installed

Start by verifying that the **Helm client** is installed. The Helm client can be installed in [different ways](https://helm.sh/docs/intro/install/) but in this case it has been already installed in our environment.

`helm version --short`{{execute}}

Use `helm -h`{{execute}} to help you  get more information about any command used through this tutorial.
