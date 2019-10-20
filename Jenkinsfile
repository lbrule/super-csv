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
                bat 'mvn -Dmaven.test.failure.ignore=true install'
                bat 'mvn  -Dmaven.test.skip=truet  versions:set  -DgenerateBackupPoms=false -DnewVersion=2.0.0'
                bat 'git add .'
                bat 'git commit -m "Test."'
                bat 'git tag -a v2.0.0'
                bat 'git push --tags'
            }
        }
   }
}
