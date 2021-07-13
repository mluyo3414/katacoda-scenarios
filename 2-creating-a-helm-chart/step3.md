**Answer:** We need to include `service.yaml`, `serviceaccount.yaml`, and `deployment.yaml` in our case for the `hello-kubernetes` application.

### Cleanup extra files not needed for simple functional chart

Let's cleanup the template and add our application YAML files (under `/root/hello-kubernetes/deploy/resources/helm)`.

* Delete the **`templates/tests`** folder and files inside:

`rm -rf /root/hello-kubernetes/deploy/resources/helm/hello-kubernetes/templates/tests/`{{execute}}

* Select and delete all the example files under **`templates`** besides **`_helpers.tpl`** file (using VSCode).

```
deployment.yaml
ingress.yaml
NOTES.txt
service.yaml
serviceaccount.yaml
```

### Adding our k8s resource files

* Select and move the `hello-kubernetes` application files: **`serviceaccount.yaml`**, **`deployment.yaml`**, and **`service.yaml`** into the **`templates/`** directory to be used by the Chart (using VSCode).

### Verify Chart structure

This is how the final configuration under `/root/hello-kubernetes/deploy/resources` should look like:
```
├── all-resources.yaml
└── helm
    └── hello-kubernetes
        ├── charts
        ├── Chart.yaml
        ├── templates
        │   ├── deployment.yaml
        │   ├── _helpers.tpl
        │   ├── serviceaccount.yaml
        │   └── service.yaml
        └── values.yaml
``` 

You can verify the folder structure by running:
`tree /root/hello-kubernetes/deploy/resources/`{{execute}}

### Question:
**Which command do we have to use to see all the files/K8s resources that our Helm Chart will create?**

Click *Continue*
