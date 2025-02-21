# Azure_Voting_Application_Using_Elastic_Kubernates_Services


This project showcases a scalable voting application built using Azure Kubernetes Service (AKS). 
The application is containerized using Docker and images are stored in Azure Container Registry (ACR). The architecture is designed with different Kubernetes pods for the application logic and the in-memory database.

Key Components
Azure Kubernetes Service (AKS): Manages and orchestrates the deployment, scaling, and operations of containerized applications.

Docker: Containerizes the application components to ensure consistent environments and simplified deployment.

Azure Container Registry (ACR): Stores and manages Docker images securely.

Application Pod: Built with Python Flask, this pod handles the voting logic and user interactions.

Redis Database Pod: Acts as an in-memory database for fast data access and storage.


![VotingAppArchDiagram](https://github.com/user-attachments/assets/e8c77caa-b715-470d-8bb1-d93f76c5bfc1)

![image](https://github.com/user-attachments/assets/10b9b23b-6e31-49e2-9d00-9530decafc3d)


Azure Container Registry (ACR) is a managed, private Docker registry service provided by Microsoft Azure. 
It allows you to store and manage container images for all types of container deployments. With ACR, you can easily build, push, and pull container images using Docker commands. The service integrates seamlessly with Azure Kubernetes Service (AKS) and other Azure services, ensuring secure and efficient management of containerized applications. ACR supports both Linux and Windows containers, and offers features such as geo-replication, vulnerability scanning, and task automation, making it a robust solution for managing container images in a secure and scalable manner.

Creating Azure Container Registry
```

az group create --name mcb-vote --location eastus
az acr create --resource-group mcb-vote --name <acrName> --sku Basic
```



![ContainerRegistrary](https://github.com/user-attachments/assets/58bcac40-0628-4c1a-886b-b6c41c22c64e)

Login ACR
```

az acr login --n <acrName> --expose-token
```

Save token and perform docker login using below command

docker login <acrName> -u 00000000-0000-0000-0000-000000000000 -p <token>


Creating docker image
```

az acr build --image mcb-vote --registry <acrName>  --file Dockerfile
```




Building Azure Kubernates Clusture 



```

az aks create \
--resource-group mcb-vote \
--name AKSClusterTCB \
--node-count 1 \
--generate-ssh-keys

```

Associate Azure Container Registratry to Azure Kubernates Clusture
```

az aks update -n AKSClusterTCB -g mcb-vote --attach-acr <acrName>  


```

Once container registratry is assoicated with Azure Kubernates Clusture
we will add get credential for Kubernates cluster
```

az aks get-credentials --resource-group mcb-vote --name AKSClusterTCB
```


We can make changes to YAML file for application configuration so it points to correct image.

Deploying the application into the cluster

![KubernatesClustres](https://github.com/user-attachments/assets/b40c65b0-3b81-4bef-aac8-35482fdb1928)


Getting public IP of load balancer,
kubectl get service --watch


Exploring the Cluster
```

kubectl get nodes
kubectl get pods

```

![KubernateServices](https://github.com/user-attachments/assets/4233fa70-799b-40ec-b8b4-74314e967807)

