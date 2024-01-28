
Copy code
# DevOps Project with Maven, Jenkins and Kubernetes

This project demonstrates the implementation of a DevOps pipeline using Maven, Jenkins and Kubernetes.

## Prerequisites

- Maven (3.6.3 or later)
- Jenkins (2.249.1 or later)
- Kubernetes (1.18 or later)

## Project Structure

- src/main/java: Contains the Java source code for the application.
- src/main/resources: Contains the configuration files for the application.
- src/test/java: Contains the Java source code for the unit tests.
- pom.xml: The Maven configuration file.

## Build and Run the Application

1. Open a terminal and navigate to the project directory.
2. Run the following command to build the application:

```bash
mvn clean package
Run the following command to run the application:
bash
Copy code
java -jar target/devops-project-1.0-SNAPSHOT.jar
Deploy the Application to Kubernetes
Create a Dockerfile in the project directory with the following content:
dockerfile
Copy code
FROM openjdk:11-jdk
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
Build the Docker image:
bash
Copy code
docker build -t devops-project .
Create a Kubernetes deployment file (devops-project-deployment.yaml) with the following content:
yaml
Copy code
apiVersion: apps/v1
kind: Deployment
metadata:
  name: devops-project
spec:
  replicas: 1
  selector:
    matchLabels:
      app: devops-project
  template:
    metadata:
      labels:
        app: devops-project
    spec:
      containers:
      - name: devops-project
        image: devops-project:latest
        ports:
        - containerPort: 8080
Deploy the application to Kubernetes:
bash
Copy code
kubectl apply -f devops-project-deployment.yaml
Setup Jenkins Pipeline
Install the necessary Jenkins plugins:

Pipeline
Docker Pipeline
Kubernetes Plugin
Create a Jenkinsfile in the project directory with the following content:

groovy
Copy code
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t devops-project .'
            }
        }
        stage('Docker Push') {
            steps {
                sh 'docker push devops-project:latest'
            }
        }
        stage('Kubernetes Deploy') {
            steps {
                sh 'kubectl apply -f devops-project-deployment.yaml'
            }
        }
    }
}
Create a new Jenkins pipeline job and configure it to use the Jenkinsfile.

Run the Jenkins pipeline job to build, test, and deploy the application.

Conclusion
This project demonstrates the implementation of a DevOps pipeline using Maven, Jenkins and Kubernetes. The pipeline includes the build, test, Docker build, Docker push, and Kubernetes deployment stages. <!--stackedit_data: eyJoaXN0b3J5IjpbLTE3MzU5MzUwMzZdfQ== -->"