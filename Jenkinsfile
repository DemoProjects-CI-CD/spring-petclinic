pipeline {
    agent { label 'MVN' }
    triggers { pollSCM('* * * * *') }
    stages {
        stage ('VCS') {
            steps {
                git url: 'https://github.com/DemoProjects-CI-CD/spring-petclinic.git',
                    branch: 'main'
            } 
        }
        stage ('build') {
            tools {
                jdk 'JDK-17'
            }
            steps {sh 'mvn package'}       
        }
        stage ('Post-build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-*.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}