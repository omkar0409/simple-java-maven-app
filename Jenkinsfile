pipeline {
    agent any
        
    stages {
        stage('Build') { 
            steps {
                sh 'docker pull maven:3-alpine'
                 
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}
