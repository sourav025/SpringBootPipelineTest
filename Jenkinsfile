pipeline {
    agent none 
    stages {
        stage('SCM') {
            agent any
            steps {
                git branch: 'master', url: 'https://github.com/sourav025/SpringBootJsp'
            }
        }
        stage('Example Build') {
            agent { docker 'maven:3-alpine' } 
            steps {
                sh 'mvn clean test install'
            }
        }
        
    }
}
