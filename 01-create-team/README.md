# Lab 1: Creating Teams

In this lab, we are going to create a Team in Otomi. Teams in Otomi serve the following purpose:

- Creating a namespace on the cluster, configuring RBAC and setting default quota's

- Provide self-service options for team members in Otomi Console

- Isolate ingress traffic between teams

- Optionally: Separate team metrics and logs. When multi-tenancy is not enabled (default), metrics and logs are not separated (providing all users admin role to see cluster wide metrics and logs)

Let's create a Team!

> **_NOTE:_** You can also check the video [here.](https://youtu.be/aNoC6OeqHKw)

## Instructions

1. In the side menu, click on `Teams` under the `Platform` section.

2. Click on `Create Team`.

3. Provide a name for the team - for the purpose of these workshops we recommend using `demo`

4. Under NetworkPolicy, disable `Network policies` and `Egress control` (we will activate this later on).

5. Leave all other settings default.

6. Click on `submit`.

7. Click on `Deploy Changes` (this will become active after in the side menu after you submit a change).

8. Select your team in the top bar. Here you can select your context (cluster and team).

9. In the side menu, the team section will now become visible.

> **_NOTE:_**

- Since we did not enable Alert manager, the Alerts section is disabled
- Since we did not enable Grafana, the Azure Monitor section is disabled

Go to the [next lab.](../02-knative/README.md)
