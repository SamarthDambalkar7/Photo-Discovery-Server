pipeline {
    agent any
    tools{
        maven 'maven_3_9_2'
    }
    stages{
        stage('Build Maven'){
           steps{
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SamarthDambalkar7/Photo-Discovery-Server']])
                 bat 'mvn clean install'
            }
        }
        stage('Build Docker Image')
        {
            steps{
                script{
                    bat 'docker build -t samarthdambalkar7/photodiscoveryserver .'
                }
            }
        }
        stage('Push Docker Image to Hub')
        {
            steps{
                script{
                    echo "Docker Hub Password: ${dockerhubpwd}"
                    withCredentials([string(credentialsId: 'DockerHub-password', variable: 'DockerHubPassword')]) {
                        bat 'docker login -u samarthdambalkar7 -p Docker@789'
                      }
                    bat 'docker push samarthdambalkar7/photodiscoveryserver'
                }
            }
        }
    }
}
