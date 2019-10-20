pipeline {
    agent any
    tools {
        maven 'Maven 3.3.9'
        jdk 'jdk8'
    }
    stages {
        stage("IC - Checkout") {
            checkout scm
        }
        stage("IC - Clean Install") {
            sh 'mvn -Dmaven.test.failure.ignore=true install'
        }
   }
}
