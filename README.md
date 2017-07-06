# rocket-chat

The docker-compose.yml available on this page [https://continuous.lu/2017/04/05/chatops-rocket-chat-hubot-bot-docker](https://continuous.lu/2017/04/05/chatops-rocket-chat-hubot-bot-docker) was converted by [Kompose](https://github.com/kubernetes-incubator/kompose) and then into one single yml.

## In Docker Compose

1.
    ```
    docker-compose -f docker-compose.yml up
    ```

## In Kubernetes

1. Create the persistent volume claim.
    ```
    kubectl apply -f rocketchat-pvc.yml
    ```

1. Verify that your persistent volume claim is created and bound to the persistent volume object. This process can take a few minutes.
    ```
    kubectl describe pvc db-claim0
    ```
    Output:

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
