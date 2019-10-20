#!groovy

/*
    job de build des projets LBPF
*/

    def String scmURLWithoutHttp;
    def scmURL = "";
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
                    echo "scm = ${scm}"
                    echo "scm = ${scm.userRemoteConfigs[0].url.replaceAll('https://','')}"
               }
            }
            stage("IC - Clean Install") {
                steps {
                    //bat 'mvn -Dmaven.test.failure.ignore=true install'
                    //bat 'mvn  -Dmaven.test.skip=truet  versions:set  -DgenerateBackupPoms=false -DnewVersion=2.0.7'
                    //bat 'git add .'
                    //bat 'git commit -m "Test."'
                    bat 'git tag -a v2.0.7-test -m "Test Tag."'
                    bat 'git tag'
                    
                    withCredentials([usernamePassword(credentialsId: '01fdcf13-8f12-47be-9a79-2e2f7a0846d0', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        bat "echo 'GIT_USERNAME = ${GIT_USERNAME}'>ludo.txt"
                        bat "echo 'GIT_PASSWORD = ${GIT_PASSWORD}'>>ludo.txt"
                        bat "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${scm.userRemoteConfigs[0].url.replaceAll('https://','')} origin v2.0.7-test"
                    }
                }
            }
       }
    }

