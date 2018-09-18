pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build image') {
            /* This builds the actual image; synonymous to
             * docker build on the command line */

            app = docker.build("simple-image")
        }

        stage('Maven build') {
            sh 'mvn -B -DskipTests clean package'
        }

        stage('Test image') {
            /* Ideally, we would run a test framework against our image.
             * For this example, we're using a Volkswagen-type approach ;-) */

            app.inside {
                sh 'echo "Tests passed"'
            }
        }

        stage('Test Maven build') {
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }

        stage('Deploy Maven build') {
            sh 'mvn deploy -P poc'
        }
    }
}