pipeline{
    agent any
    tools{
        maven 'maven_3.5.0'
    }
    stages{
        stage("Build Maven"){
            steps{
               checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/parthu19/spring-boot-docker']]])
               bat 'mvn clean install'
            }
        }
        stage("Build docker image"){
            steps{
                script{
                    bat 'docker build -t parthkadia/spring-boot-docker .'
                }
            }
        }
        stage("Push image to hub"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpws')]) {
                        bat 'docker login -u parthkadia -p Parth@@123'
                        bat 'docker push parthkadia/spring-boot-docker'
                    }
                }
            }
        }
    }
}