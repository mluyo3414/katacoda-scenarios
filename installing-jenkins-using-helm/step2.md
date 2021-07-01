Now, let's explore the [Jenkins Helm Chart](https://github.com/jenkinsci/helm-charts/tree/main/charts/jenkins). First, we need to add the public  repository to be able to pull the chart and also update to get the latest information. 

`helm repo add jenkins https://charts.jenkins.io`{{execute}}
`helm repo update`{{execute}}

We can check the available versions executing: 

`helm search repo jenkins/jenkins --versions`{{execute}}

In this case, we are going to install the chart version 3.4.0 and then we will update it in a later step. Helm gives us the option to customize the installation by either passing different values in the command line or creating a YAML file with the options.

Let's find which values the Jenkins Chart allows us to modify.

`helm show values jenkins/jenkins`{{execute}}

An easier way to see all the options, is to save them in a file.

`helm show values jenkins/jenkins > values.yaml`{{execute}}

You can see the values.yaml in VSCode as it is saved in the local environment.