
# 🐳 Django CI/CD Pipeline with Jenkins & Docker

📌 This project demonstrates a Complete CI/CD workflow for a Django Notes App using Jenkins, Docker, and Ubuntu servers. It automates the process of building, testing, and deploying containerized applications — ideal for learning or implementing modern DevOps pipelines.
## 🏗 Architecture

- Server Setup: We will use 2 EC2 instances for this project. You can also use VM/Azure/GCP.
- Master Node: Runs Jenkins and Java, exposes required ports 21, 80, and 8080
- Slave Node: Runs Java and Docker, allows the same ports, and is connected securely via SSH keys with the master server.
- Code source: hosted on GitHub and pulled during the pipeline (we will be using the Django Notes app).

- Deployment: Managed with Docker Compose on the target server.
## Project Diagram

[![cicd.png](https://i.postimg.cc/vHfQwqTp/cicd.png)](https://postimg.cc/3drMgZgB)


## EC2 Setup
We will set up 2 EC2 instances:
 - Both will run Ubuntu Server 24.04
 - One will be the master and the other the slave
 - The master server will create automation scripts with Jenkins, and the slave server will execute them.
[![1.png](https://i.postimg.cc/L592kfjN/1.png)](https://postimg.cc/1njks8Cq)

Add Those server in a same security group and allow those port 
- 80-http
- 8080-jenkins
- 8000-django note app
[![1.png](https://i.postimg.cc/L592kfjN/1.png)](https://postimg.cc/1njks8Cq)



## Server Setup

Conenct both instance by ssh.
- ###  Master server setup.
```bash
    sudo apt update
    sudo apt upgrade -y
```
 Install Java and Jenkins
   ```bash
        # Install Java (required by Jenkins)
sudo apt install -y fontconfig openjdk-17-jre

# Add Jenkins key
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

# Add Jenkins repository
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/" | \
  sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

# Update package list
sudo apt update

# Install Jenkins
sudo apt install -y jenkins

   ```
- ### Now, access Jenkins Master on the browser on port 8080 and configure it.

- ### Slave server setup.

``` bash
     sudo apt update
     sudo apt upgrade -y
     sudo apt install fontconfig openjdk-17-jre -y
     sudo apt install docker.io
     sudo apt install docker-compose
```
- ### Now Add a node(slave server) in jenkins
- ### Create a New Job Build and it will be a pipeline job task.

``` bash
     pipeline {
    agent { label 'agent' }

    stages {

        stage('Clone Code') {
            steps { 
                echo 'Cloning the repository...'
                git url: 'https://github.com/tushar4560/django-cicd-jenkins.git', branch: 'main'
                echo 'Code cloned successfully.'
            }
        }

        stage('Build Image') {
            steps { 
                echo 'Building Docker image...'
                sh 'docker build -t notes-app:latest .'
                echo 'Docker image built successfully.'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running Django tests using CI settings...'
                sh """
                    docker run --rm \
                      -v \$(pwd):/app/backend \
                      -w /app/backend \
                      notes-app:latest \
                      sh -c "python manage.py test --settings=notesapp"
                   """
                   echo 'Cleaning up dangling Docker images...'
                sh """
                    docker images -f dangling=true -q | xargs -r docker rmi || true
                   """
                   echo 'Tests completed.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh """
                     docker-compose up -d
                   """
                echo 'Deployment complete.'
            }
        }
    }
}
```

[![5.png](https://i.postimg.cc/XNZm8zTM/5.png)](https://postimg.cc/DmTxfBv5)

[![6.png](https://i.postimg.cc/76jBdqjF/6.png)](https://postimg.cc/vgLL6wYh)


## As you can see, the CI/CD pipeline is complete.This is a basic CI/CD project using Jenkins.

### If anyone has questions, feel free to ask me.
