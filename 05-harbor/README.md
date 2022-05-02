# Lab 5: Working with Harbor

In this lab, you are going to:

1. Activate Harbor
2. Create a robot account
3. Build an image and push it to Harbor in Otomi
4. Create a Kubernetes Deployment and Service
5. Publicly expose the Hello World app using Otomi

When you create a Team in Otomi, Otomi will automatically create a project for the team in Harbor. In this lab, we'll assume you have created a team called `demo`.

> **_NOTE:_** When running Otomi on Minikube you might not have enough resources for this lab.

## Instructions

### 1. Activate Harbor

Go to `Apps` under the `Platform` section in the side menu and Drag and Drop `Harbor` from the `Disabled apps` to the `Enabled apps`.

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

3. Download the demo application used in this tutorial

<<<<<<< Updated upstream
    ```bash
    # Clone the repo used for this tutorial
    git clone https://github.com/redkubes/nodejs-helloworld.git
    ```
||||||| constructed merge base
1. Download the demo application used in this tutorial
=======
### 3. Download and build the demo application used in this tutorial
>>>>>>> Stashed changes

<<<<<<< Updated upstream
4. Log in to Harbor
||||||| constructed merge base
- Clone the repo used for this tutorial:

```bash
git clone https://github.com/redkubes/nodejs-helloworld.git
```

4. Login to Harbor
=======
Clone the repo used for this tutorial:

```bash
git clone https://github.com/redkubes/nodejs-helloworld.git
```

docker built -t `harbor.<yourdomain>`
### 4. Login to Harbor
>>>>>>> Stashed changes

Login with username `otomi-team-demo-push` and password: `token`

<<<<<<< Updated upstream
    ```bash
    docker login -u 'otomi-team-demo-push' -p '$token' harbor.<your-domain>
    ```
||||||| constructed merge base
```bash
docker login -u 'otomi-team-demo-push' -p '$token' harbor.<your-domain>
```
=======
```bash
docker login -u 'otomi-team-demo-push' -p $token harbor.<your-domain>
```
>>>>>>> Stashed changes

### 5. Build, tag and push the image

<<<<<<< Updated upstream
    ```bash
    # Build and tag the image
    docker build -t harbor.<your-domain>/team-demo/hello-world:latest .
    ```
||||||| constructed merge base
- Build and tag the image:

```bash
docker build -t harbor.<your-domain>/team-demo/hello-world:latest .
```

- Push the image to Harbor:
=======
1. Build and tag the image:

```bash
docker build -t harbor.<your-domain>/team-demo/hello-world:latest .
```

2. Push the image to Harbor:
>>>>>>> Stashed changes

    ```bash
    # Push the image to Harbor
    docker push harbor.<your-domain>/team-demo/hello-world:latest
    ```

Now go to the `team-demo` project and verify that the `hello-world` repository has been created.

Go to the [next lab](../06-secrets/README.md)
