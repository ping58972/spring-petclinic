pipeline {
    agent any
    triggers {
        pollSCM 'H/2 * * * *'
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
    }
}
