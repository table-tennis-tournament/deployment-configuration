# Table Tennis Tournament Deployment Configuration
This repository contains all OpenShift deployment configuration of the table tennis tournament software. The configuration is brought into the cluster by  [Argo CD](https://argoproj.github.io/argo-cd/). 

# Getting Started
The deployments of Table Tennis Tournament are deployed in OpenShift. To interact with OpenShift via CLI, you need the appropriate [Client Tools](https://www.okd.io/download.html).

All members of the [Table Tennis Tournament](https://github.com/orgs/table-tennis-tournament/people) organisation can login via GitHub at the following applications:

* [OpenShift Cluster](https://console.baloise.dev)
* [Argo CD](https://argocd.baloise.dev)

To get access to the deployed applications, add the GitHub username in the `namespaces/values.yaml` file under `namespaces.users`. 

# Deploy Application
To deploy an application in the OpenShift cluster, a `Helm Chart` must be created. You can use the [generic chart]()

## Create Helm Chart
To create a `Helm Chart`, simply copy the `app-template` directory into a new one, e.g. `rocket-app-stage`.  Then open the `rocket-app-stage/Chart.yaml` file, and change the `name: app-template` to the newly created directory name to `name: rocket-app-stage`. 

Then change the referenced `image.repository` and `image.tag` under `app.frontend` and `app.backend` in the `rocket-app-stage/values.yaml` file.

Congratulation, you created and configured your `Helm Chart`.

## Reference Helm Chart
To deploy your newly created `Helm Chart` in OpenShift you need to reference your `Chart` in the `namespaces/values.yaml` file. To add a new entry at `namespaces.applications` list. After you pushed your commit, it takes around 30 secounds until the deployment in OpenShift starts. You should see the Deployment in the [ArgoCD Web Console](https://argocd.wheel.sh). Your deployed app will then be accessable under https://rocket-app-stage.apps.wheel.sh (replace rocket-app-stage with actual directory/Chart name) if not declared otherwise. 

### Reference Helm Chart

```
namespaces:
[...]
  applications:
[...]
    - name: rocket-app-stage # Must be the same as the directory name.   
      helm: 
        valueFiles:
          - "values.yaml"
      # This enables automatic synchronization from Git.           
      syncPolicy:
        automated:
          prune: true
```

### References YAML
If you want to deploy simply from YAML files, you can just declare the `name` attribute which must match the directory name:

```
namespaces:
[...]
  applications:
[...]
    - name: rocket-app-stage # Must be the same as the directory name.   
      # This enables automatic synchronization from Git.           
      syncPolicy:
        automated:
          prune: true
```
