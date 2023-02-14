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
        stage("unit testing"){
            steps{
                
                sh 'mvn test'
            }
            post{
                success{
                     echo "junit testing is success,publishing report"
                     junit 'target/surefire-reports/*.xml'
                
                }
                failure{
                    echo "junit testing is failed"

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
                        -Dsonar.host.url=http://ec2-43-207-130-215.ap-northeast-1.compute.amazonaws.com:9000/
                        -Dsonar.login=sqp_99ba142b04460fe6d488b6b743acc168e871c6a8"
                    }
                }
            }
        }
        stage('upload artifact'){
            steps{
                script{
                    sh 'mvn -s settings.xml deploy'
                }
            }
        }
    }
}