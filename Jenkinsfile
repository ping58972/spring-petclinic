pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('docker show') {
            steps {
                sh 'docker --version'
                sh 'git --version'
                sh 'brew list'
            }
        }
        stage('git pull') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ping58972/spring-petclinic.git']]])
            }
        }
        stage('compile test package') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('junit and artifacts') {
            steps {
                junit '**/target/surefile-reports/TEST-*.xml'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
