pipeline {
    agent any
    tools {
        maven 'MAVEN_3.9'
    }
    stages {
        stage('build'){
            steps{
                 script{
                    echo "maven code build"
                    sh 'mvn clean install'
                }
            }
           
        }
    }
}