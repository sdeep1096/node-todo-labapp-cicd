pipeline{
    agent{
        label 'dev-agent'
    }

    stages{
        stage('code'){
            steps{
                git url: 'https://github.com/sdeep1096/node-todo-labapp-cicd.git' , branch: 'main'
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t briarheart1096/node-todo-labapp-cicd:latest'
            }
        }
        stage('Login and Push Image'){
            steps{
                echo "Logging in to Docker hub"
                withCredentials([usernamePassword(credentialsId:'DockerHub',passwordVariable:'DockerHubPassword',usernameVariable:'DockerHubUsername')]){
                    sh "docker login -u ${env.DockerHubUsername} -p ${env.DockerHubPassword}"
                    sh "docker push briarheart1096/node-todo-labapp-cicd:latest"
                }
            }
        }
        stage('Deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
