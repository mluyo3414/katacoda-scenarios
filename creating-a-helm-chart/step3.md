Let's cleanup the template and add our application YAML files (under `/root/hello-kubernetes/deploy/resources/helm)`.

* Delete the **`templates/tests`** folder inside:

`rm -rf /root/hello-kubernetes/deploy/resources/helm/hello-kubernetes/templates/tests/`{{execute}}

* Select and delete everything on **`templates`** besides **`_helpers.tpl`** file (using VSCode).

* Move the **`serviceaccount.yaml`**, **`deployment.yaml`**, and **`service.yaml`** into the **`templates/`** directory to be used by the Chart (using VSCode).


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

* Inspect the `Chart.yaml` file. Notice how there is a `version` for the chart version and a `appVersion` for the application version itself.

Go to the `cd /root/hello-kubernetes/deploy/resources/helm/hello-kubernetes/`{{execute}} directory and test that the chart can be rendered `helm template [NAME] [FOLDER]`:

`helm template hello-kubernetes . | less`{{execute}}

You should see all the resources that Helm will create (the same as the resource files we copied into `/templates`). Press `q` to exit from the view.

