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
