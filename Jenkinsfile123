pipeline {
    agent any
    tools{
    maven 'maven'    
    }

    stages {
        stage('checkout ') {
            steps {
               git branch: 'development', credentialsId: 'ff3328aa-302a-4006-a8c6-cb998687bf56', url: 'https://github.com/KandlaguntaVenkataSivaNiranjanReddy/maven-web-app-project-kk-funda.git'
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean package'  
            }  
        }
        stage('sonar') {
            steps {
                sh 'mvn sonar:sonar'  
            }  
        }
        stage('upload artifact') {
            steps {
                sh 'mvn deploy'  
            }  
        }
        stage('Deploy') {
            steps {
                sshagent(['aad79589-071e-4e85-a192-2020a02c8e8d']) {
                    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.60.79.198:/opt/apache-tomcat-9.0.91/webapps/"
                }  
            }  
        }
    }
}
