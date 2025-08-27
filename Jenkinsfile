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
