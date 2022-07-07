# Lab 6: Create and use secrets using Hashicorp Vault

In this lab, you are going to create a secret in Hashicorp Vault.

## Instructions

### 1. Activate Vault

Go to `Apps` under the `Platform` section in the side menu and Drag and Drop `Vault` from the `Disabled apps` to the `Enabled apps` and `Deploy Changes`.

### 2. Create a secret in Vault

- Open `Vault`
- Sign in with Method `OIDC`, click on `Sign in with OIDC Provider` and leave `role` blank

You are now automatically redirected to the team space `teams/team-demo/`created in Vault.

- Click on `Create secret`
- Provide a name for the secret. We'll use the name hello. The name of the secret will be: `teams/team-demo/hello`
- In the key field, fill in `TARGET`
- In the value field, fill in `party people`
- Click on `save`

The secret is now created in vault. In the next tutorial, you are going to "inject" the secret in the Otomi service configuration.

Now we need to synchronize the secret in Vault to Kubernetes so the secret can be used in workloads.

### 3. Create a secret in Otomi:

- In the left panel under the Team demo, click `Secrets`
- Click on `Create secret`
- Provide a name for the secret. The name should match the name of the secret in Vault. Use the name `hello`
- Select `Generic` (default)
- Under `Entries` fill in `TARGET` (the key of the secret in Vault)
- Click `submit`
- Click on `Deploy Changes` in the left pane of the console

Note: Under the hood, an open-source tool called `external-secrets` is at work that will transform a Vault secret into a regular Kubernetes secret.

The secret in Vault is now mapped and can be used by the team in any workload. Otomi Console makes this easy by offering a secret selector during the creation of services.

### 4. Create a new K8s deployment that uses the secret

- Install the hello resources:

    ```bash
    kubectl apply -f https://raw.githubusercontent.com/redkubes/workshops/main/08-secrets/hello-svc.yaml -n team-$TEAM-NAME
    ```

- Go to `Services`
- Click `New Service`
- Fill in `hello-svc` as the name of the service
- Select `Existing Kubernetes service`
- Under `Exposure` select `Ingress`
- Apply & Deploy Changes

