# Table Tennis Tournament Deployment Configuration
This repository contains all OpenShift deployment configuration of the table tennis tournament software. The configuration is brought into the cluster by  [Argo CD](https://argoproj.github.io/argo-cd/). 

# Getting Started
The deployments of Table Tennis Tournament are deployed in OpenShift. To interact with OpenShift via CLI, you need the appropriate [Client Tools](https://www.okd.io/download.html).

All members of the [Table Tennis Tournament](https://github.com/orgs/table-tennis-tournament/people) organisation can login via GitHub at the following applications:

* [OpenShift Cluster](https://console.baloise.dev)
* [Argo CD](https://argocd.baloise.dev)

To get access to the deployed applications, add the GitHub username in the `namespaces/values.yaml` file under `namespaces.users`. 

# Deploy Application
To deploy an application in the OpenShift cluster, a `Helm Chart` must be created. You can use the [generic chart](https://github.com/baloise-incubator/generic-chart)

## kubeseal
To seal the secrets with kubeseal, you can use the following scripts:
### ttt-registration
```
kubectl create secret generic email-sealed-secrets --dry-run --from-literal=emailserver='?' --from-literal=emailuser='?' --from-literal=emailpassword='?' -o yaml >mysecret.yaml
```
```
kubeseal --namespace=ttt-registration --cert https://raw.githubusercontent.com/baloise-incubator/okd4-cluster-infra-apps/master/sealed-secrets/kubeseal.crt -oyaml <mysecret.yaml >email-sealed-secrets.yaml 
```
