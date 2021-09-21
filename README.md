
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


