# Table Tennis Tournament Deployment Configuration
This repository contains all deployments of the table tennis tournament software in OpenShift. The configuration is brought into the cluster via [ArgoCD](https://argoproj.github.io/argo-cd/). 

# Getting Started
The deployments of Table Tennis Tournament are deployed in OpenShift. To interact with OpenShift, you need the appropriate [Client Tools](https://www.okd.io/download.html).

All members of the [Table Tennis Tournament](https://github.com/orgs/table-tennis-tournament/people) organisation can register via GitHub at the following sites

* [OpenShift Cluster](https://console.wheel.sh:8443)
* [ArgoCD](https://argocd.wheel.sh)

# Deploy Application
To deploy an application in the OpenShift cluster, a `Helm Chart` must be created, and this must reference in the `namespaces/values.yaml` file.

## Create Helm Chart
To create a Helm Chart, simply copy the `app-template` directory into a new one, e.g. "rocket-app-stage". 