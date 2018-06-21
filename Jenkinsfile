pipeline {
    agent any
    
     tools { 
        maven 'Maven 3.3.9' 
        jdk 'jdk8' 
    }
    
    stages {
        
       stage ('Initialize') {
            steps {
                
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                
            }
       }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
  stage('SonarQube analysis') {
   steps {
              withSonarQubeEnv('My SonarQube Server') {
                sh 'mvn clean package sonar:sonar'
              }
            
  }
  }
        stage('Test') { 
            steps {
                sh 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
    }
}
