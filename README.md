

mvn clean package -f spring-petclinic/pom.xml<br />
mvn clean package -f OwnerService/pom.xml<br />
mvn clean package -f PetService/pom.xml<br />
mvn clean package -f VetService/pom.xml<br />
mvn clean package -f VisitService/pom.xml<br />


ls -alt spring-petclinic/target/*.jar <br />
ls -alt OwnerService/target/*.jar <br />
ls -alt PetService/target/*.jar <br />
ls -alt VetService/target/*.jar <br />
ls -alt VisitService/target/*.jar <br />


docker build  --squash -t egapm/spring-petclinic:frontend-svc -f spring-petclinic/Dockerfile spring-petclinic/.<br />
docker build  --squash -t egapm/spring-petclinic:owners-svc -f OwnerService/Dockerfile OwnerService/.<br />
docker build  --squash -t egapm/spring-petclinic:pets-svc -f PetService/Dockerfile PetService/.<br />
docker build  --squash -t egapm/spring-petclinic:vets-svc -f VetService/Dockerfile  VetService/.<br />
docker build  --squash -t egapm/spring-petclinic:visits-svc -f VisitService/Dockerfile  VisitService/.<br />
docker build --squash -t egapm/spring-petclinic:mysql-db -f mysql/Dockerfile mysql/.<br />


docker push egapm/spring-petclinic:frontend-svc<br />
docker push egapm/spring-petclinic:pets-svc <br />
docker push egapm/spring-petclinic:owners-svc<br />
docker push egapm/spring-petclinic:vets-svc<br />
docker push egapm/spring-petclinic:visits-svc<br />
docker push egapm/spring-petclinic:mysql-db<br />

