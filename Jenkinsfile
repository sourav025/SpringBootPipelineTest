node {
    stage('Configure') {
        version = '1.1'
        currentBuild.displayName = version

        properties([
                buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '10')),
                [$class: 'GithubProjectProperty', displayName: '', projectUrlStr: 'https://github.com/bertjan/spring-boot-sample/'],
                pipelineTriggers([[$class: 'GitHubPushTrigger']])
            ])
    }

    stage('Checkout') {
        git 'https://github.com/bertjan/spring-boot-sample'
    }

    stage('Version') {
        sh "echo \'\ninfo.build.version=\'$version >> src/main/resources/application.properties || true"
        sh "mvn -B -V -U -e versions:set -DnewVersion=$version"
    }

    stage('Build') {
        sh 'mvn -B -V -U -e clean package'
    }

    stage('Archive') {
        junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
    }

    stage('Deploy') {
        // Depends on the 'Credentials Binding Plugin'
        // (https://wiki.jenkins-ci.org/display/JENKINS
        sh 'echo \'\nBuild Completed. Test echo. Find jar at /var/lib/jenkins/worksspace\''
    }
}
