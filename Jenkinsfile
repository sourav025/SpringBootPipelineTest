pipeline {
    agent none 
    stages {
        stage('SCM') {
            agent any
            steps {
                git branch: 'master', url: 'https://github.com/sourav025/SpringBootJsp'
                sh 'ls -ls'
            }
        }
        stage('Example Build') {
            agent { docker 'maven:3-alpine' } 
            steps {
                sh 'ls -ls'
                sh 'mvn --version'
            }
        }
    }
}
