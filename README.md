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

 `kubectl get deployment argo-server`
 
 `kubectl describe deployment nginx-deployment`

 `kubectl scale deployment/nginx-deployment --replicas=10`


 ## LoadBalancer 

  ### Enable ingress using below command 
  `minikube addons enable ingress`
  
   By default external port will be pending you need to hit below command in seperate cmd to update
   `minikube tunnel`

### Start Config Map Dashboard
   `minikube dashboard`

 ### minikube command

 minikube start

 minikube start --driver=virtualbox

minikube service erps-redis-cache-service-svc


   kubectl logs erps-redis-cache-service-deployment-c55449bf8-rzsch

   ### Delete minikube
    minikube delete
