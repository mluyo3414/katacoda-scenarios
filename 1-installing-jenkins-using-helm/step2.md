Now, let's explore the [Jenkins Helm Chart](https://github.com/jenkinsci/helm-charts/tree/main/charts/jenkins). First, we need to follow the documentation and add the public repository to be able to pull the chart. We also update to get the latest chart information. 

`helm repo add jenkins https://charts.jenkins.io`{{execute}}

`helm repo update`{{execute}}

Before we run any other command, let's create a namespace to deploy Jenkins:

`kubectl create ns jenkins`{{execute}}

**Note: The `| less` option was added to most commands so you can scroll through the terminal. Exit that view mode by pressing `q`.**

We can check the available versions by running: 

`helm search repo jenkins/jenkins --versions | less`{{execute}}

Notice there are two versions, one is the Helm chart `3.3.21` version and the other one is the application version itself `2.277.4`. In this case, we are going to install the chart version `3.3.21`. Helm gives us the option to customize the installation with different settings.

Let's find which values the Jenkins Chart allows us to modify (the options shown are the **default** chart options).

`helm show values jenkins/jenkins --version 3.3.21 | less`{{execute}}

An easier way to see all the **default** options, is to save them in a file.

`helm show values jenkins/jenkins --version 3.3.21 > values.yaml`{{execute}}

You can see the `values.yaml` in VSCode as it is saved in the top level of the local environment. Scroll to the bottom of all files.

Now that you have seen which values can be used to customize the installation, what command you think you will you use to install the application? Use `helm -h`{{execute}} and analyze different options. Click *Continue* to see the correct answer.


