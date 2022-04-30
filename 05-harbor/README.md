# Lab 5: Working with Harbor

In this lab, you are going to:

- Activate Harbor
- Build an image and push it to Harbor in Otomi
- Create a Kubernetes Deployment and Service
- Publicly expose the Hello World app using Otomi

When you create a Team in Otomi, Otomi will automatically create a project for the team in Harbor. In this lab we'll assume you have created a team called `demo`.

> **_NOTE:_** You can not do this lab when running Otomi on Minikube!

## Instructions

1. Activate Harbor

- Go to `Apps` under the `Platform` section in the side menu and Drag and Drop `Harbor` from the `Disabled apps` to the `Enabled apps`.

2. Create a robot account in Harbor

> **_NOTE:_** Robot accounts for teams can only be created by users with the `otomi-admin` role

- Open `Harbor`
  
- Click `Login with OIDC Provider`
  
- Fill in your user name and click save
  
- Under `Administration`, click `Robot Accounts`
  
- Click on `+ New Robot account`
  
- Provide a name for the new robot account: `team-demo-push`
  
- Set an Expiration time
  
- Select `team-demo` and optionally change the permissions

- Click `Add`

- Copy the generated token


1. Download the demo application used in this tutorial

- Clone the repo used for this tutorial:

```bash
git clone https://github.com/redkubes/nodejs-helloworld.git
```

4. Login to Harbor

- Login with username `otomi-team-demo-push` & password: `token`

```bash
docker login -u 'otomi-team-demo-push' -p '$token' harbor.<your-domain>
```

5. Build, tag and push the image

- Build and tag the image:

```bash
docker build -t harbor.<your-domain>/team-demo/hello-world:latest .
```

- Push the image to Harbor:

```bash
docker push harbor.<your-domain>/team-demo/hello-world:latest
```

Now go to the team-demo project and verify that the hello-world repository has been created.

Go to the [next lab](../06-secrets/README.md)