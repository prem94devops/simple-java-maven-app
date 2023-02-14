pipeline {
    agent any
    tools {
        maven 'MAVEN_3.9'
    }
    stages {
        stage('build'){
            script{
                sh 'mvn clean install'
            }
        }
    }
}