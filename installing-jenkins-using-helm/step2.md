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

You can see the `values.yaml` in VSCode as it is saved in the top level of the local environment.

We are going to set the **application storage** to **false** since our ephemeral working environment does not offer a persistent volume and it will cause an error in our deployment. In order to do that, we need to change the `persistent` option to `false`. You can locate this option  ** in or around line 707** in `values.yaml` or search for the following block:

```
persistence:
  enabled: true
```

There are two ways we can customize the installation of the Jenkins chart with this option. 

One option is to pass different values in the command line (we are going to also execute the `--dry-run` as we are not installing yet):

`helm install jenkins jenkins/jenkins -n jenkins --version 3.3.21 --set persistence.enabled=false --dry-run`{{execute}}

Another option is to pass the `values.yaml` file with the options (preferred method as the file can be saved in version control). Go to the `values.yaml` file we exported in VSCode and only keep the option we want to change (**Yes, delete the rest** - Helm will only change the persistent option to false and deploy all the rest of **default** options):

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