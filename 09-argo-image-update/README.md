# Lab 9: Using Argo image updater

In this lab we are going to:

- Add a Helm Chart to Harbor
- Connect Argo CD to the chart repository in Harbor
- Create an application in Argo CD to deploy the chart
- Configure the application to automatically update the container images of the workload managed by Argo CD

## Prerequisites

- Harbor is enabled
- Argo CD is enabled
- A team in Otomi is created

## Instructions

1. Add a chart to Harbor
  
- Open the Harbor app (when signed in as `otomi-admin`)

- In the `Library` project, click on `Helm Charts`

- Download the `hello-0.1.1.tgz` file

2. Connect the repository in Argo CD

- Open Argo CD

- In `Settings`, click on `Repositories`
  
- Click on `Connect Repo using https`
  
- Type = `Helm`
  
- Project = `Harbor`
  
- Repository URL = `harbor.<your-domain>/chartrepo/library`
  
- Click `Connect`

3. Create a new application in Argo CD

- Under applications, click on `Create`

- Application Name = `Hello`

- Project = `<team-name>`

- Sync Policy = `Automatic`

- Repository URL = `harbor.<your-domain>/chartrepo/library` (we be shown automatically)

- Chart = `hello`

- Version = `0.1.0`

- Cluster URL = `https://kubernetes.default.svc`

- Namespace = `<team-name>`

- Click on `Create`

You will see that that the hello application is now automatically deployed. To see the app, create a new Service in Otomi (in the team where the app is deployed) and set the exposure ingress to `public`.

1. Configure automatic image updates

- In Argo CD, go to applications and click on the `hello` application
  
- Click on `App Details` and then `Edit`
  
- Under `Annotations`, add the following annotation:

```yaml
argocd-image-updater.argoproj.io/image-list:otomi/nodejs-helloworld:~1.2
```
- Now click `Save`

The image version that is deployed using the chart is `1.2.12`. The `otomi/nodejs-helloworld` however contains an image with version `1.2.13`. Now go to the URL of the hello service and refresh the page. What do you see?