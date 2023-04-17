pipeline{
    agent { label 'dev-agent' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/Manish12588/node-to-cicd.git', branch: 'main'
            }
        }
         stage('Build and Test'){
            steps{
                echo "Building and Testing..."
                sh 'docker build . -t manish12588/node-todo-app-cicd:latest'
            }
        }
         stage('Login and Push Image'){
            steps{
                echo "Pushing Image to Docker hub..."
                withCredentials([usernamePassword(credentialsId:'dockerHub',usernameVariable:'dockerHubUser',passwordVariable:'dockerHubPassword')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push manish12588/node-todo-app-cicd:latest"
                }
            
            }
        }   
        stage('Deploy'){
            steps{
                echo "Deploying application..."
                sh 'docker-compose down && docker-compose up -d'
            }
        }
        
    }
}
