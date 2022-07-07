# Lab 5: Working with Harbor

In this lab, you are going to:

1. Activate Harbor
2. Create a robot account
3. Login to Harbor
4. Build an image and push it to Harbor in Otomi

When you create a Team in Otomi, Otomi will automatically create a project for the team in Harbor. In this lab we'll assume you have created a team called `demo`.

> **_NOTE:_** When running Otomi on Minikube you might not have enough resources for this lab.

## Instructions

### 1. Activate Harbor

Go to `Apps` section under the `Platform` section in the side menu and Drag and Drop `Harbor` from the `Disabled apps` to the `Enabled apps` and `Deploy Changes`

### 2. Create a robot account in Harbor

**_NOTE:_** Robot accounts for teams can only be created by users with the `otomi-admin` role

1. Open `Harbor`
2. Click `Login with OIDC Provider`
3. Fill in your user name and click save
4. Under `Administration`, click `Robot Accounts`
5. Click on `+ New Robot account`
6. Provide a name for the new robot account: `team-demo-push`
7. Set an Expiration time
8. Select `team-demo` and optionally change the permissions
9. Click `Add`
10. Copy the generated token


### 3. Login to Harbor

Log out of Harbor then click "Login via Local DB" with username `otomi-team-demo-push` and password: `<token>`

```bash
docker login -u 'otomi-team-demo-push' -p <token> harbor.<your-domain>
```

> **_NOTE:_** If Docker refuses to connect with an error
`x509: certificate signed by unknown authority`, go to the Otomi Console,
and click `Download CA` (if you have not done so already); then copy the
obtained file to `~/.docker/ca.crt` or restart docker desktop.

### 4. Download, build and push the demo application

Clone the repo used for this tutorial:

```bash
git clone https://github.com/redkubes/nodejs-helloworld.git && cd nodejs-helloworld/
```

Build and tag the image:

```bash
docker build -t harbor.<your-domain>/team-demo/hello-world:latest .
```

Push the image to Harbor:

```bash
docker push harbor.<your-domain>/team-demo/hello-world:latest
```

Now go to the team-demo project and verify that the hello-world repository has been created.

Go to the [next lab](../06-secrets/README.md)
