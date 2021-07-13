
### Adding a Chart to our local environment 

As we mentioned before, a chart is a set of files ( compressed `tgz`) needed to deploy the application in Kubernetes. We are going to need to download it to our local environment so that it can be installed in K8s. 

Let's explore the [Jenkins Helm Chart](https://github.com/jenkinsci/helm-charts/tree/main/charts/jenkins). First, we need to follow the documentation and add the public repository to be able to pull the chart using `helm repo add`. We will name our local repository `jenkins` and provide the URL with the public location of the repo `https://charts.jenkins.io`.

We also update to get the latest chart information. 

`helm repo add jenkins https://charts.jenkins.io`{{execute}}

`helm repo update`{{execute}}

### Finding different versions of the Jenkins Chart 

**Note: The `| less` option was added to most commands so you can scroll through the terminal. Exit that view mode by pressing `q`.**

Inside that repo (which we named `jenkins`), we will search for the `jenkins` chart (hence `jenkins/jenkins` - `repo/chart`). We can search for the available chart versions by running: 

`helm search repo jenkins/jenkins --versions | less`{{execute}}

Again, `jenkins/jenkins` is the name of the repo and the name of the chart. 

`--version` will provide us all the available versions. 

Notice there are two versions in each line, one is the Helm chart version (i.e `3.3.21`) and the other one is the application version itself (i.e `2.277.4`). In this case, we are going to install the chart version `3.3.21`. 

Before we run any other command, let's create a [namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces) in Kubernetes to deploy Jenkins:

`kubectl create ns jenkins`{{execute}}

### How can you customize a chart installation?

Let's find which values the Jenkins Chart allows us to modify (the options shown with the below commands are the **default** chart options). These options allow us to customize our installation (i.e which Docker image to use for the controller, how much RAM/CPU the pod should use, etc). 

`helm show values jenkins/jenkins --version 3.3.21 | less`{{execute}}

An easier way to see all the **default** options, is to save them in a file. 

`helm show values jenkins/jenkins --version 3.3.21 > values.yaml`{{execute}}

You can see the `values.yaml` in VSCode as it is saved in the top level of the local environment. Scroll to the bottom of all files. Feel free to read all the available options in the `values.yaml` file.

### Question:

**Now that you have seen which values can be used to customize the installation, what command you think you will use to deploy the application?** 

Use `helm -h`{{execute}} and search for different options. 

Click *Continue* to see the correct answer.


