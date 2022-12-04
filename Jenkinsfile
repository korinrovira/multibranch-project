pipeline {
    agent {
        label 'nodo-1'
    }

    stages {

        stage('Compilacion') {
            steps {
               sh 'mvn -D skipTests clean install package'
            }
        }

        stage('Unit test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                   junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker image build -t webapp-ucreativa .'
            }
        }

        stage('Tag docker image') {
            steps {
                sh 'docker image tag webapp-ucreativa korinrovira/webapp-ucreativa:latest'
            }
        }

        stage('Upload docker image') {
            steps {
                sh 'docker login -u korinrovira -p &t33lD00r928+'
                sh 'docker image push korinrovira/webapp-ucreativa:latest'
            }
        }
    }
}
