# Simple Notes App
This is a simple notes app built with React and Django.

## Requirements
1. Python 3.9
2. Node.js
3. React

## jenkins steps

Permission for setup jenkins(sometimes you can see some error and using these cmd you can quickly fix issue) 
```
sudo chmod -aG docker $USER
sudo chmod -aG docker jenkins

sudo chown $USER /var/run/docker.sock
sudo chmod 777 /var/run/docker.sock

```
1. Clone the repository
```
stage('code cloned'){
                steps {
                    git url: "https://github.com/Hemantjangir53/django-notes-app", branch: "main"
                    echo 'clode cloned successfully'
                }
            }
```

2. Build the app
```
stage('Build'){
                steps {
                    sh 'docker build . -t django-notes-app'
                    echo 'code build'
                }
            }
```

3. push to dockerHub
```
stage('push to docker Hub') {
            steps {
                withCredentials([
                        usernamePassword(
                            credentialsId: 'dockerHub',
                            usernameVariable: 'DOCKER_USERNAME',
                            passwordVariable: 'DOCKER_PASSWORD')]){
                                
                                sh "docker tag node-todo-app ${env.DOCKER_USERNAME}/node-todo-app:latest"
                                sh "docker login -u ${env.DOCKER_USERNAME} -p ${env.DOCKER_PASSWORD}"
                                sh "docker push ${env.DOCKER_USERNAME}/node-todo-app:latest"
                                
                    }
                
                echo "code push"
            }
        }
```

4. Run the app
```
stage('Deploy'){
                steps{
                  //  sh 'docker run -d -p 8000:8000 hemantjangir/django-notes-app:latest'
                    sh 'docker-compose down && docker-compose up -d'
                    echo "deployed the container"
                }
            }
```
![Screenshot from 2023-12-20 19-33-33](https://github.com/Hemantjangir53/django-notes-app/assets/146804084/6b41ecf8-823b-4573-85c4-abaa09c29258)





