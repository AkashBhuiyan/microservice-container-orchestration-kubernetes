# Kubernetes Dashboard

This image shows the Kubernetes Dashboard with deployed microservices.

![Kubernetes Dashboard](K8s-dashboard.png)

# Kubernetes Dashboard Documentation

[K8s Dashboard Documentation](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)

## Helm Installation
[Helm Installation Guide](https://helm.sh/docs/intro/install/)

## Dashboard Installation
```sh
helm upgrade --install kubernetes-dashboard kubernetes-dashboard/kubernetes-dashboard --create-namespace --namespace kubernetes-dashboard
```

## Port Forwarding for Dashboard Access
```sh
kubectl -n kubernetes-dashboard port-forward svc/kubernetes-dashboard-kong-proxy 8443:443
```

## Create Dashboard Admin User
```sh
kubectl apply -f dashboard-adminuser.yaml
```

## Role Binding for Admin User
```sh
kubectl apply -f dashboard-rolebinding.yaml
```

## Create Secret for Admin User
```sh
kubectl apply -f secret.yml
```

## Create Token for Admin User
```sh
kubectl -n kubernetes-dashboard create token admin-user
```

## Create Bearer Token for Access by a Single Token
```sh
kubectl get secret admin-user -n kubernetes-dashboard -o jsonpath="{.data.token}" | base64 -d
```

## Kubernetes Commands
```sh
kubectl get deployments
```
```sh
kubectl get services
```
```sh
kubectl get replicaset
```
```sh
kubectl get pods
```
```sh
kubectl describe pod <pod-name>
```
```sh
kubectl logs <pod-name>
```
```sh
kubectl get pods -o wide
```

## Create Docker Images from the Git Project

Follow the steps mentioned in this link repository to create Docker images for this Kubernetes project from the Git repository: [microservice-architecture-java](https://github.com/AkashBhuiyan/microservice-architecture-java).

## Create Environment Variable in Kubernetes Cluster
```sh
kubectl apply -f configmaps.yml
```

## Order of Deployment
To ensure services are deployed in a structured manner, the following order should be followed:

1. **Keycloak** - Identity and access management service.
2. **ConfigMaps** - Configuration for environment variables and other settings.
3. **ConfigServer** - Centralized configuration management service.
4. **EurekaServer** - Service registry for microservices.
5. **accountsdb** - Database for microservices.
6. **cardsdb** - Database for microservices.
7. **loandb** - Database for microservices.
8. **Accounts** - Microservice handling account-related operations.
9. **Loan** - Microservice managing loan-related functionalities.
10. **Cards** - Microservice handling card-related processes.
11. **Gateway** - API Gateway for routing requests to services.

## Deploying Applications in Kubernetes
To deploy microservices and applications in a Kubernetes cluster, the appropriate YAML manifest files should be created and applied. Each microservice and configuration must be properly defined before deployment.

### Deployment Commands
```sh
kubectl apply -f keycloak.yml
```
```sh
kubectl apply -f configserver.yml
```
```sh
kubectl apply -f eurekaserver.yml
```
```sh
kubectl apply -f accountsdb.yml
```
```sh
kubectl apply -f cardsdb.yml
```
```sh
kubectl apply -f loandb.yml
```
```sh
kubectl apply -f accounts.yml
```
```sh
kubectl apply -f loan.yml
```
```sh
kubectl apply -f cards.yml
```
```sh
kubectl apply -f gateway.yml
```

## Scale Deployments
```sh
kubectl scale deployment accounts-deployment --replicas=2
```

## Retrieves detailed information about the specified Pod and Displays its status, events, conditions, logs, and resource usage.
```sh
kubectl describe pod <pod-name>
```

## Updates the container image and Triggers a rolling update
```sh
kubectl set image deployment/<deployment-name> <container-name>=<new-image-name>:<new-image-tag>
```
> Example:
> ```sh
> kubectl set image deployment gatewayserver-deployment gatewayserver=akash9229/gatewayserver:v2
> ```

## Rolling Update
```sh
kubectl rollout restart deployment <deployment-name>
```

## Check if the new image is being used:
```sh
kubectl get deployment gatewayserver-deployment -o wide
```

## Retrieves and displays Kubernetes events in the default namespace, sorted by creation time (oldest first), helping debug issues and track cluster activities and events.
```sh
kubectl get events -n default --sort-by=.metadata.creationTimestamp
```

## Delete a Pod
```sh
kubectl delete pod <pod-name>
```

## Delete a Deployment
```sh
kubectl delete deployment <deployment-name>
```

## Delete a Service
```sh
kubectl delete service <service-name>
```

## View Logs for a Pod Continuously
```sh
kubectl logs -f <pod-name>
```

## View Resource Utilization of Pods
```sh
kubectl top pod
```

## View Resource Utilization of Nodes
```sh
kubectl top node
```

## Check Running Namespaces
```sh
kubectl get namespaces
```

## Get All Resources in a Namespace
```sh
kubectl get all -n <namespace>
```

## Apply All Configurations in a Directory
```sh
kubectl apply -f ./k8s/
```

## Troubleshooting: Debug a Failing Pod
```sh
kubectl exec -it <pod-name> -- /bin/sh
```

## Restart a Pod
```sh
kubectl delete pod <pod-name> --grace-period=0 --force
```

## Check the Current Context
```sh
kubectl config current-context
```

## Switch Kubernetes Contexts
```sh
kubectl config use-context <context-name>
