pipeline{
    agent any

    environment{
        DOCKERHUB_CREDENTIALS=credentials('docker_hub')
        NEXUS_CREDENTIALS = credentials('nexus')
        
    }

    stages{
        
        stage('Build'){

            steps{
                sh 'docker build -t Helloapp .'
            }

        }

        stage('Login'){
            steps{
                sh 'echo $NEXUS_CREDENTIALS_PSW | docker login -u $NEXUS_CREDENTIALS_USR --password-stdin http://localhost:8085/repository/docker-private-repo/'
            }

        }
        stage('Push'){

            steps{
                sh 'docker tag Helloapp:latest localhost:8085/docker-private-repo/Helloapp:latest'
                sh 'docker push localhost:8085/docker-private-repo/my-app:latest'
            }

        }
    }
    post{
        always{
            sh 'docker logout'
        }
    }
}