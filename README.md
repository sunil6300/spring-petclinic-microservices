# Spring Petclinic App - SpringBoot Based Microservices
 Deploy petclinic app with eG BTM monitoring enabled.
 
## Pre-Requisites
 - git
 - java 8
 - maven 3.5.0+
 - docker
   - Ensure that docker cli pre-configured with docker registry to push the images.
 - kubectl/ocp 
   - Ensure that kubectl/ocp cli pre-configured with cluster.

   
## Clone

    git clone https://github.com/eginnovations/spring-petclinic-microservices.git
    cd spring-petclinic-microservices
    
## [Optional] Update eG RUM Script In The Frontend App
    vi spring-petclinic/src/main/resources/templates/fragments/layout.html

## Build Application Jars

    mvn clean package -f spring-petclinic/pom.xml  
    mvn clean package -f OwnerService/pom.xml  
    mvn clean package -f PetService/pom.xml  
    mvn clean package -f VetService/pom.xml  
    mvn clean package -f VisitService/pom.xml

## Build Docker Images

    docker build --squash -t egapm/spring-petclinic:frontend-svc -f spring-petclinic/Dockerfile spring-petclinic/.  
    docker build --squash -t egapm/spring-petclinic:owners-svc -f OwnerService/Dockerfile OwnerService/.  
    docker build --squash -t egapm/spring-petclinic:pets-svc -f PetService/Dockerfile PetService/.  
    docker build --squash -t egapm/spring-petclinic:vets-svc -f VetService/Dockerfile VetService/.  
    docker build --squash -t egapm/spring-petclinic:visits-svc -f VisitService/Dockerfile VisitService/.  
    docker build --squash -t egapm/spring-petclinic:mysql-db -f mysql/Dockerfile mysql/.

## Push Docker Images

    docker push egapm/spring-petclinic:frontend-svc  
    docker push egapm/spring-petclinic:pets-svc  
    docker push egapm/spring-petclinic:owners-svc  
    docker push egapm/spring-petclinic:vets-svc  
    docker push egapm/spring-petclinic:visits-svc  
    docker push egapm/spring-petclinic:mysql-db
    
## Create PullSecret To Avoid Docker Hub Pull Request Limitation    

    kubectl create secret generic regcred \
    --from-file=.dockerconfigjson=/root/.docker/config.json \
    --type=kubernetes.io/dockerconfigjson
    
## Update eG Manager Details In The eG Agent Daemonset Yaml
    vi k8s/eg-agent/egagent.yaml
        
## Deploy eG Agent Into Kubernetes/OpenShift
    kubectl apply -f k8s/eg-agent/.
 
## Deploy Microservices Into Kubernetes/OpenShift
    
    # Petclinic App
    kubectl apply -f k8s/app/namespace_and_service_account/.
    kubectl apply -f k8s/app/db/.
    kubectl apply -f k8s/app/.
    
## Delete Microservices From Kubernetes/OpenShift
    # Petclinic App
    kubectl delete -f k8s/app/namespace_and_service_account/.
    kubectl delete -f k8s/app/db/.
    kubectl delete -f k8s/app/.

## Delete eG Agent From Kubernetes/OpenShift
    # eG Agent
    kubectl delete -f k8s/eg-agent/.
