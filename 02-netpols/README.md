# Lab 2: Configuring network policies

In this lab we are going to deploy a multi tier web application, called `guestbook`, register the 3 K8s services in Otomi and configure public access to the `frontend` service. Next, we will turn on the `Network policies` option for the team.

## Instructions

1. Install the Guestbook application resources:

```bash
kubectl apply -f https://raw.githubusercontent.com/redkubes/workshops/main/02-netpols/guestbook.yaml -n team-$TEAM-NAME
```

2. Get the names of the created ClusterIP services:

```bash
kubectl get svc -n team-<$TEAM-NAME>
```

You will see 3 services:

```bash
NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
frontend         ClusterIP   10.0.183.235   <none>        80/TCP     6m44s
redis-follower   ClusterIP   10.0.135.61    <none>        6379/TCP   6m44s
redis-leader     ClusterIP   10.0.82.226    <none>        6379/TCP   6m44s
```

3. Go to Otomi Console. Make sure you have selected your team in the top bar en and then click the `Services` item under your team in the side menu.

4. We will now first add the created frontend service to Otomi. Click `Create Service`.

5. Fill in the name `frontend`.

6. Under `Exposure`, select `Public`. Leave all other settings under exposure default.

7. Leave all other settings default and click `submit`.

8. Click `Deploy Changes`.

**INFO**: After the changes have been deployed (this will take a couple of minutes), you will see that the service we just created has a host name. Click on the host name to get access to the `guestbook` frontend. Submit a few messages on the application. 

9. Register the `redis-follower` and `redis-leader` services via the otomi-console. Make sure to provide the correct port (6379) and leave all other settings default (so no exposure) and `submit`. You don't need to `Deploy Changes` after every submit.

**INFO**: When you create a service in Otomi with ingress `Cluster`, the K8s service will be added to the service-mesh in Otomi. When you create services in Otomi, the Istio Gateway is automatically configured and Istio virtual services are also automatically created.

 *Notice that the guestbook frontend still works!*

10. In Otomi Console go to your team and then click the `Settings` item.

11. Under Network policy, enable `Network policies`. Click `submit` and then `Deploy Changes`

**INFO**: Now go to the Guestbook application and notice that your messages have disappeared and you can't submit new messages. This is because traffic between the `frontend` and the `redis-leader` and `redis-follower` services is not permitted anymore. 

*Let's fix this*

12. In the otomi-console, click on the `redis-leader` service.

13. Under `Network policies`, select `Allow selected` and click `add item`. Add the following 2 items and Submit:

| Team name   | Service Name |
| ----------- | ------------ |
| $TEAM-NAME   | frontend     |
| $TEAM-NAME   | redis-follower |

Before deploying changes, go to the `redis-follower` service and do the same, but in this case only allow the frontend service:

| Team name   | Service Name |
| ----------- | ------------ |
| $TEAM-NAME   | frontend    |
| $TEAM-NAME   | redis-leader |

Now `Deploy Changes`

Notice that the Guestbook app works again.

Go to the [next lab](../03-activate-apps/README.md)
