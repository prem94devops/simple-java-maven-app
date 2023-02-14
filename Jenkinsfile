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
        stage('sonar'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'SONAR_TOKEN') {
                    sh "${tool("SONARQUBE")}/bin/sonar-scanner \
                        -Dsonar.projectKey=simple-java-maven-app \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=target \
                        -Dsonar.host.url=http://ec2-35-79-22-198.ap-northeast-1.compute.amazonaws.com:9000/ \
                        -Dsonar.login=sqp_99ba142b04460fe6d488b6b743acc168e871c6a8"
                    }
                }
            }
        }
    }
}