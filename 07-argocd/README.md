# Lab 7: Working with Argo CD

In this lab we are going to show how easy it is for a team to sync a gitops repo in Otomi with Argo CD. We will also configure the image autoupdater plugin to auto-update the image tag of the workload if it matches a defined pattern.

When Gitea is enabled, Otomi creates a gitops repo named `team-$Name-argocd` for each team, and deploys the necessary Argo CD CRs to make the repo sync with the team namespace automatically. No Argo configuration is therefor needed for this workshop.

The steps are as follows:

1. Upload a chart to Harbor
2. Connect a team's helm repo in Argo CD
3. Create an Argo CD app of type `Helm` and see it sync
4. Add image auto-update configuration to make the workload's image update when new patch versions are published

## Prerequisites

1. You are familiar with Argo CD concepts
2. Harbor is enabled in Otomi. (Check the `Apps` section under `Platform`.)
3. One team is created. We will refer to it as `team-demo`.
4. You have followed [Lab 5: Working with Harbor](./../05-harbor/README.md).

## Instructions

### 1. Upload a chart to Harbor

You can do this in the Harbor UI, or directly with the helm CLI:

Login to the team's OCI registry first, by using the credentials created in [Lab 5: Working with Harbor](./../05-harbor/README.md)

```
helm registry login -u 'otomi-team-demo-push' -p $token harbor.<your-domain>
```

Upload the provided `hello-0.1.0.tgz` chart:

```
helm push ./hello-0.1.0.tgz oci://harbor.<your-domain>/library/hello
```


### 2. Connect a team's helm repo in Argo CD

1. Open `Settings` > `Repositories`
2. Choose `Connect Repo using https`
3. Input the following:
   - `Type: Helm`
   - `Name: Harbor`
   - `Project: <team-name>`
   - `Repository URL: https://harbor.<your-domain>/chartrepo/library`
4. Click `Connect`

### 3. Create an Argo CD application

1. Select `Applications`, and click on `Create`
2. Input the following:
   - `Application Name: hello`
   - `Project: <team-name>`
   - `Sync Policy: Automatic`
   - `Repository URL: harbor.<your-domain>/chartrepo/library`
   - `Chart: hello`
   - `Version: 0.1.0`
   - `Cluster URL: https://kubernetes.default.svc`
   - `Namespace: <team-name>`
3. Click on `Create`

You will see that that the hello application is now automatically deployed. To see the app, create a new Service in Otomi (in the team where the app is deployed) and set the exposure to `Ingress`.

### 4. Configure Argo CD Image Updater

1. In Argo CD, go to applications and click on the `hello` application
2. Click on `App Details` and then `edit`
3. Under `Annotations`, add the following annotation:

```yaml
argocd-image-updater.argoproj.io/image-list: "otomi/nodejs-helloworld:~1.2"
```

4. Now click `Save`

The image version that is deployed using the chart is `1.2.12`. The `otomi/nodejs-helloworld` however contains an image with version `1.2.13`. Now go to the URL of the hello service and refresh the page. What do you see?


Go to the [next lab.](../08-secrets/README.md)