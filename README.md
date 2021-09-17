cd /opt/openshift_lab/spring-petclinic-manual-microservices

mvn clean package -f spring-petclinic/pom.xml
mvn clean package -f OwnerService/pom.xml
mvn clean package -f PetService/pom.xml
mvn clean package -f VetService/pom.xml
mvn clean package -f VisitService/pom.xml


ls -alt spring-petclinic/target/*.jar 
ls -alt OwnerService/target/*.jar 
ls -alt PetService/target/*.jar 
ls -alt VetService/target/*.jar 
ls -alt VisitService/target/*.jar 


docker build  --squash -t egapm/spring-petclinic:frontend-svc -f spring-petclinic/Dockerfile spring-petclinic/.
docker build  --squash -t egapm/spring-petclinic:owners-svc -f OwnerService/Dockerfile OwnerService/.
docker build  --squash -t egapm/spring-petclinic:pets-svc -f PetService/Dockerfile PetService/.
docker build  --squash -t egapm/spring-petclinic:vets-svc -f VetService/Dockerfile  VetService/.
docker build  --squash -t egapm/spring-petclinic:visits-svc -f VisitService/Dockerfile  VisitService/.
docker build --squash -t egapm/spring-petclinic:mysql-db -f mysql/Dockerfile mysql/.


docker push egapm/spring-petclinic:frontend-svc
docker push egapm/spring-petclinic:pets-svc 
docker push egapm/spring-petclinic:owners-svc
docker push egapm/spring-petclinic:vets-svc
docker push egapm/spring-petclinic:visits-svc
docker push egapm/spring-petclinic:mysql-db

