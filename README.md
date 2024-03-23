# App Monolitica CI Y CD
El pipeline se encuentra en el job __spring-framework-petclinic__

- __Build__
    - Se realiza el empaquetado en un file .war
- __Testing__
    - El informe de cobertura generado por Jacoco está disponible en http://54.191.82.56:8080/job/agoncal-application-petstore-ee7/lastBuild/jacoco/

- __Sonarqube__
    - Se analiza la calidad del código, cuyos resultados pueden consultarse http://54.191.82.56:9000/dashboard?id=org.agoncal.application%3Apetstoreee7
    ![sonarqube](./screenshots/sonarqube.png)        

- __Artifactory__
    - Los artefactos están almacenados en un repositorio Jfrog, accesible a través de http://54.191.82.56:8082/ui/repos/tree/General/petstoreee7-release/org.agoncal.application/petstoreee7/7.1/applicationPetstore.war
    ![artifactory](./screenshots/artifactory.png)       

- __Deploy Jobss (Ansible)__
    - La app monolito se despliega en la siguiente URL: http://35.87.76.96:8080/applicationPetstore
    ![deployed](./screenshots/deployed.png)    


__Nota:__ Los accesos para Sonar, Jenkins y Jfrog se encuentran detallados en el correo electrónico enviado previamente.
