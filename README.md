# docker_k8s_command

### Docker command

```docker images```

```docker image build -t sampleapp:latest .```

Get Docker Info 

 ```Docker info```

### sync minikube with docker

   eval $(minikube docker-env)

 ### Kubectl command

 kubectl get pods

 kubectl get svc or services

 kubectl get nodes

 kubectl get deployments

 kubectl get replicaset

##### `kubectl scale --replicas=1 deployment finance-ui-app-deployment`
##### `kubectl apply -f deployments.yaml`
`kubectl describe deployments`

 ### minikube command

 minikube start

minikube service erps-redis-cache-service-svc


   kubectl logs erps-redis-cache-service-deployment-c55449bf8-rzsch
