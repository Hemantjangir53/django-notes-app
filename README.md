# Simple Notes App
This is a simple notes app built with React and Django.

## Requirements
1. Python 3.9
2. Node.js
3. React

## jenkins steps
1. Clone the repository
```
git clone https://github.com/Hemantjangir53/django-notes-app.git
```

2. Build the app
```
docker build -t notes-app .
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
docker run -d -p 8000:8000 notes-app:latest
```
![Screenshot from 2023-12-20 19-33-33](https://github.com/Hemantjangir53/django-notes-app/assets/146804084/6b41ecf8-823b-4573-85c4-abaa09c29258)





