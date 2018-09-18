pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    stages {
        stage('MASTER build') {
            when {
                branch 'master'
            }
            steps {
                sh 'mvn -P poc clean deploy'
            }
        }
        stage('BRANCH build') {
            when {
                not { branch 'master' }
            }
            steps {
                sh 'mvn -P poc clean package'
            }
        }
    }

}