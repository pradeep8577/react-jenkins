pipeline{
    agent any
    environment{
        imageName = "pradeep018/react-app"
        registryCredential = "pradeep018"
        dockerImage= ""
    }
    stages{
        stage('Clone'){
            steps{
                git ' https://github.com/pradeep8577/react-jenkins.git'
            }
        }
        stage('Install'){
            steps{
                sh 'npm install'
            }
        }
        stage('Build'){
            steps{
                sh 'npm run build'
            }
        }
        stage('Docker Build'){
            steps{
                script{
                    dockerImage = docker.build imageName
                }
            }
        }
        stage('Docker Push'){
            steps{
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-creds'){
                        dockerImage.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }
    }
}