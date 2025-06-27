# Netflix Clone – Full DevOps Deployment & Monitoring

This project demonstrates a complete end-to-end DevOps pipeline for deploying a Netflix Clone application, including CI/CD, security scanning, containerization, monitoring, and Kubernetes orchestration. Below are the detailed steps and tools used throughout the process.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Step 1: Launch EC2 Instance](#step-1-launch-ec2-instance)
- [Step 2: Install Jenkins, Docker, and Trivy](#step-2-install-jenkins-docker-and-trivy)
- [Step 3: TMDB API Key Setup](#step-3-create-a-tmdb-api-key)
- [Step 4: Install Prometheus & Grafana](#step-4-install-prometheus-and-grafana)
- [Step 5: Jenkins Monitoring with Prometheus](#step-5-install-the-prometheus-plugin-and-integrate-it-with-the-prometheus-server)
- [Step 6: Jenkins Email Integration](#step-6-email-integration-with-jenkins-and-plugin-setup)
- [Step 7: Jenkins Plugins & Pipeline Setup](#step-7-install-plugins-like-jdk-sonarqube-scanner-nodejs-owasp-dependency-check)
- [Step 8: SonarQube Integration](#step-8-configure-sonar-server-in-manage-jenkins)
- [Step 9: Security Scanning (OWASP & Trivy)](#step-9-install-owasp-dependency-check-plugins)
- [Step 10: Docker Build & Push](#step-10-docker-image-build-and-push)
- [Step 11: Kubernetes Setup & Deployment](#step-11-kuberenetes-setup)
- [Step 12: Monitoring & Access](#step-12-access-from-a-web-browser)
- [Step 13: Cleanup](#step-13-terminate-instances)
- [Complete Jenkins Pipeline](#complete-jenkins-pipeline)

---

![Screenshot 2025-06-27 at 9 18 23 AM](https://github.com/user-attachments/assets/5d06ba27-6915-4697-8a9a-cc8cf5b8cc07)
![Screenshot 2025-06-27 at 9 18 45 AM](https://github.com/user-attachments/assets/538325c3-aabf-4241-bbfd-643ec198ecf8)
![Screenshot 2025-06-27 at 9 19 16 AM](https://github.com/user-attachments/assets/509fda1e-dfb5-4f01-8f54-37e6d0627f8c)



## Project Overview
This repository contains a Netflix Clone application built with React and TypeScript. The project demonstrates a robust DevOps workflow, including CI/CD automation, code quality checks, security scanning, containerization, monitoring, and deployment to Kubernetes.

---

## Step 1: Launch EC2 Instance
- Launch an AWS EC2 T2 Large instance with Ubuntu 22.04.
- Enable HTTP/HTTPS in the Security Group and open all ports (for learning/demo purposes).

---

## Step 2: Install Jenkins, Docker, and Trivy
### Jenkins Installation
- Install Jenkins using a shell script (`jenkins.sh`).
- Open port 8080 for Jenkins access.
- Unlock Jenkins, install suggested plugins, and create an admin user.

### Docker Installation
- Install Docker and add your user to the `docker` group.
- Run SonarQube in a Docker container for code quality analysis.

### Trivy Installation
- Install Trivy for vulnerability scanning of filesystems and Docker images.

---

## Step 3: Create a TMDB API Key
- Register at [TMDB](https://www.themoviedb.org/) and generate an API key for the application.

---

## Step 4: Install Prometheus and Grafana
- Create system users for Prometheus and Node Exporter.
- Download and configure Prometheus for metrics collection.
- Install and configure Node Exporter for system metrics.
- Install Grafana for metrics visualization and connect it to Prometheus.
![Screenshot 2025-06-27 at 5 49 53 AM](https://github.com/user-attachments/assets/3bf86ee1-f0c3-4afc-8a90-6df8b5367dc3)

---

## Step 5: Install the Prometheus Plugin and Integrate it with the Prometheus Server
- Install the Prometheus plugin in Jenkins.
- Add Jenkins as a target in Prometheus for monitoring.
- Import Grafana dashboards for Jenkins metrics visualization.
![Screenshot 2025-06-27 at 5 54 13 AM](https://github.com/user-attachments/assets/4358783a-6dd8-4d7d-a7af-c04b376ccd91)
![Monituring After Pipeline Build](https://github.com/user-attachments/assets/af7ce1d8-e50a-4ca1-9531-d76e65a5a66e)

---

## Step 6: Email Integration With Jenkins and Plugin Setup
- Install the Email Extension plugin in Jenkins.
- Configure Gmail with app passwords for Jenkins notifications.
- Set up email notifications in Jenkins pipeline for build results and reports.
![Screenshot 2025-06-27 at 6 05 31 AM](https://github.com/user-attachments/assets/2d818779-c23d-4a58-b8d1-6f4d90bc57eb)
![Screenshot 2025-06-27 at 6 05 51 AM](https://github.com/user-attachments/assets/de7213b9-d2ba-4e20-944f-0003c67f16b3)

---

## Step 7: Install Plugins like JDK, SonarQube Scanner, NodeJs, OWASP Dependency Check
- Install required Jenkins plugins: Eclipse Temurin Installer, SonarQube Scanner, NodeJs, OWASP Dependency-Check.
- Configure Java and Node.js in Jenkins Global Tool Configuration.
- Create a Jenkins pipeline job for the Netflix Clone.

---

## Step 8: Configure Sonar Server in Manage Jenkins
- Run SonarQube on port 9000 and generate a token for Jenkins integration.
- Add SonarQube server and token in Jenkins credentials and system configuration.
- Set up webhooks for quality gate status notifications.
![Screenshot 2025-06-27 at 6 41 23 AM](https://github.com/user-attachments/assets/d6f21cb9-edf8-476d-afb1-4d6051f24d0f)
![Screenshot 2025-06-27 at 6 42 08 AM](https://github.com/user-attachments/assets/fda9598e-2f14-4812-bc44-5ad70a9c18d2)

---

## Step 9: Install OWASP Dependency Check Plugins
- Install and configure the OWASP Dependency-Check plugin in Jenkins.
- Add pipeline stages for OWASP and Trivy filesystem scans.
![OWASP_TRIVY_Pipeline_Build_SuccessFull](https://github.com/user-attachments/assets/5075ab00-2170-489a-8e6b-29bffa4b12d8)

---

## Step 10: Docker Image Build and Push
- Install Docker-related plugins in Jenkins.
- Add DockerHub credentials in Jenkins.
- Add pipeline stages to build, tag, and push Docker images.
- Run Trivy image scan and store results.
- Deploy the container locally for validation.
![Screenshot 2025-06-27 at 8 16 55 AM](https://github.com/user-attachments/assets/91e5a730-c416-4e6b-9229-470518eee276)

---

## Step 11: Kubernetes Setup
- Set up two Ubuntu instances (master and worker) for Kubernetes.
- Install Docker and Kubernetes tools on both.
- Initialize the cluster, set up networking (Flannel), and configure `kubectl`.
- Install the Kubernetes plugin in Jenkins and add credentials.
- Install Node Exporter on both master and worker for monitoring.
- Add both nodes as targets in Prometheus.
- Add pipeline stages to deploy the app to Kubernetes using manifests.

---

## Step 12: Monitoring & Access
- Access Prometheus and Grafana dashboards for system and Jenkins metrics.
- Access the deployed Netflix Clone via the public IP and service port.

---

## Step 13: Terminate Instances
- Clean up by terminating AWS EC2 instances when done.

---

## Complete Jenkins Pipeline
Below is the Jenkins pipeline script used for the entire process:

```groovy
pipeline{
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/Aj7Ay/Netflix-clone.git'
            }
        }
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Netflix \
                    -Dsonar.projectKey=Netflix '''
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-token' 
                }
            } 
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        stage('OWASP FS SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP-Check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){   
                       sh "docker build --build-arg TMDB_V3_API_KEY=YOUR_TMDB_API_KEY -t netflix ."
                       sh "docker tag netflix yourdockerhub/netflix:latest "
                       sh "docker push yourdockerhub/netflix:latest "
                    }
                }
            }
        }
        stage("TRIVY"){
            steps{
                sh "trivy image yourdockerhub/netflix:latest > trivyimage.txt" 
            }
        }
        stage('Deploy to container'){
            steps{
                sh 'docker run -d --name netflix -p 8081:80 yourdockerhub/netflix:latest'
            }
        }
        stage('Deploy to kubernets'){
            steps{
                script{
                    dir('Kubernetes') {
                        withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                                sh 'kubectl apply -f deployment.yml'
                                sh 'kubectl apply -f service.yml'
                        }   
                    }
                }
            }
        }
    }
    post {
     always {
        emailext attachLog: true,
            subject: "'${currentBuild.result}'",
            body: "Project: ${env.JOB_NAME}<br/>" +
                "Build Number: ${env.BUILD_NUMBER}<br/>" +
                "URL: ${env.BUILD_URL}<br/>",
            to: 'your-email@example.com',
            attachmentsPattern: 'trivyfs.txt,trivyimage.txt'
        }
    }
}
```

---

## Credits
- Original Netflix Clone: [jason-liu22/netflix-clone-react-typescript](https://github.com/jason-lu22/netflix-clone-react-typescript)
- DevOps Pipeline, Monitoring, and Documentation: Anshuman Mohapatra

---

## License
This project is for educational and demonstration purposes. 
