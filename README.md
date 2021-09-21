# Spring Petclinic App - SpringBoot Based Microservices
## Pre-Requisites
 - git
 - java 8
 - maven 3.5.0+
 - docker
 - docker login : docker should be pre-configured with docker registry to push the images

   
## Clone

    git clone https://github.com/eginnovations/spring-petclinic-microservices.git


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

