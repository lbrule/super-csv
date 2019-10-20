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
                     script {
                      //bat 'mvn -Dmaven.test.failure.ignore=true install'
                    //bat 'mvn  -Dmaven.test.skip=truet  versions:set  -DgenerateBackupPoms=false -DnewVersion=2.0.8'
                    //bat "mvn -X -Dmaven.javadoc.skip=true --batch-mode release:clean release:prepare release:perform"
                    //bat 'git add .'
                    //bat 'git commit -m "Test."'
                    bat 'git tag -a v2.0.8-test -m "Test Tag."'
                    bat 'git tag'
                    bat 'git remote show origin'
                    bat "git config --global user.email 'ludovic.brule@gmail.com'"
                    bat "git config --global user.name 'ludovic.brule@gmail.com'"
                    //bat 'git config --global --unset https.proxy'
                    //bat 'git config --global --unset http.proxy'
                    //bat "git push origin v2.0.8-test"
                    
                    withCredentials([usernamePassword(credentialsId: '01fdcf13-8f12-47be-9a79-2e2f7a0846d0', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                      //  bat "echo 'GIT_USERNAME = ${GIT_USERNAME}'>ludo.txt"
                       // bat "echo 'GIT_PASSWORD = ${GIT_PASSWORD}'>>ludo.txt"
                        bat "git rebase origin/master"
                        bat "git push -v --all"
                    }
                }
            }
       }
        }

}
    def getDevVersion() {
        //def gitCommit = bat(returnStdout: true, script: 'git rev-parse HEAD').trim()
        def gitCommit = bat "git rev-parse HEAD"
	    echo "gitCommit = ${gitCommit}"
        def versionNumber;
 	    echo "env.BUILD_NUMBER = ${env.BUILD_NUMBER}"
       if (gitCommit == null) {
            versionNumber = env.BUILD_NUMBER;
        } else {
            versionNumber = gitCommit.take(8);
        }
        echo 'build  versions...'
	    echo "versionNumber = ${versionNumber}"
        return versionNumber
    }

    def getReleaseVersion() {
        def pom = readMavenPom file: 'pom.xml'
        def gitCommit = bat "returnStdout: true, script: 'git rev-parse HEAD'"
	    echo "gitCommit = ${gitCommit}"
        def versionNumber;
        if (gitCommit == null) {
            versionNumber = env.BUILD_NUMBER;
        } else {
            versionNumber = gitCommit.take(8);
        }
	    echo "versionNumber = ${versionNumber}"
        return pom.version.replace("-SNAPSHOT", ".${versionNumber}")
    }
