pipeline {
    agent any
    tools {
        maven 'Maven 3.3.9'
        jdk 'jdk8'
    }
    stages {
        stage("IC - Checkout") {
            steps {
                checkout scm
            }
        }
        stage("IC - Clean Install") {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
        }
   }
}
