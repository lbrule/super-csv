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
                    bat 'mvn -Dmaven.test.failure.ignore=true install'
                    bat 'mvn  -Dmaven.test.skip=truet  versions:set  -DgenerateBackupPoms=false -DnewVersion=2.0.1'
                    bat 'git add .'
                    bat 'git commit -m "Test."'
                    bat 'git tag -a v2.0.1-test -m "Test Tag."'
                    withCredentials([usernamePassword(credentialsId: 'e6d21786-af14-4eff-b65e-fd682ccdf65e', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        bat "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${scm.userRemoteConfigs[0].url.replaceAll('https://','')} origin v2.0.1-test"
                    }
                }
            }
       }
    }

