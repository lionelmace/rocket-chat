# rocket-chat

The docker-compose.yml available on this page [https://continuous.lu/2017/04/05/chatops-rocket-chat-hubot-bot-docker](https://continuous.lu/2017/04/05/chatops-rocket-chat-hubot-bot-docker) was converted by [Kompose](https://github.com/kubernetes-incubator/kompose) and then into one single yml.

# Run Rocket.Chat with Docker Compose

1. Run Rocket.Chat with docker-compose
    ```
    docker-compose -f docker-compose.yml up
    ```


# Deploy Rocket.Chat in Kubernetes on Bluemix

## Step 1 - Deploy Rocket.Chat in a lite cluster

1. Perform the steps 1 to 4 available on this [tutorial](https://github.com/lionelmace/bluemix-labs/tree/master/labs/Lab%20Kubernetes%20-%20Orchestrate%20your%20docker%20containers). In Step 3, make sure to follow Step 3.1 Create a Lite Cluster.

1. Deploy Rocker.Chat
    ```
    kubect create -f rocketchat-kube-nodeport-novolume.yml
    ```

## Step 2 - Deploy Rocket.Chat in a standard cluster

1. Perform the steps 1 to 4 available on this [tutorial](https://github.com/lionelmace/bluemix-labs/tree/master/labs/Lab%20Kubernetes%20-%20Orchestrate%20your%20docker%20containers).  In Step 3, make sure to follow Step 3.2 Create a Standard Cluster.

1. Create the persistent volume claim.
    ```
    kubectl apply -f rocketchat-pvc.yml
    ```

1. Verify that your persistent volume claim is created and bound to the persistent volume object. This process can take a few minutes.
    ```
    kubectl describe pvc db-claim0
    ```

1. Access your cluster

    ```
    bx cs cluster-get lionel-cluster-fra
    ```
    Output
    ```
    Retrieving cluster lionel-cluster-fra...
    OK

    Name:			lionel-cluster-fra
    ID:			ae2d2177ec0a4d17a2d669847e281027
    State:			normal
    Created:		2017-06-29T15:08:18+0000
    Datacenter:		fra02
    Master URL:		https://169.50.56.174:20423
    Ingress subdomain:	lionel-cluster-fra.eu-central.containers.mybluemix.net
    Ingress secret:		lionel-cluster-fra
    Workers:		2
    Log Space:		79f34553-c223-44c9-8fa2-c31c32d6eb67

    Addons
    Name            Enabled
    basic-ingress   true
    ```

1. In the file `rocketchat-kube-ingress.yml`, replace the host value on line 43 by the Ingress subdomain in the output above:
    ```
    - host: lionel-cluster-fra.eu-central.containers.mybluemix.net
    ```

1. Deploy Rocket.Chat
    ```
    kubect create -f rocketchat-kube-ingress.yml
    ```

1. Access Rocket.Chat with the URL
    `<ingress-domain>:3000`
