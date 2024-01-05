pipeline {
    agent any 
    stages {
        stage('code clone') {
            steps {
                git url: "https://github.com/Hemantjangir53/django-notes-app.git", branch: "main"
                echo "code cloned successfully"
            }
        }
        stage('Build') {
            steps {
                sh 'docker build . -t node-todo-app'
                echo "code build successfully"
            }
        }
        stage('push to docker Hub') {
            steps {
                
                withCredentials([
                        usernamePassword(
                            credentialsId: 'dockerHub',
                            usernameVariable: 'DOCKERHUB_USERNAME',
                            passwordVariable: 'DOCKERHUB_PASSWORD')]){
                                sh "docker tag node-todo-app ${env.DOCKERHUB_USERNAME}/node-todo-app:latest" // image tag
                                sh "docker login -u ${env.DOCKERHUB_USERNAME} -p ${env.DOCKERHUB_PASSWORD}"
                                sh "docker push ${env.DOCKERHUB_USERNAME}/node-todo-app:latest"  // image name-> <dockerhub_user_name>/image_name
                    }
                
                echo "code push"
            }
        }
        stage('deploy') {
            steps {
                //sh "docker run -d -p 8000:8000 hemantjangir/node-todo-app:latest"
                sh 'docker-compose down && docker-compose up -d'
                echo "container deploy"
            }
        }
    }
}
