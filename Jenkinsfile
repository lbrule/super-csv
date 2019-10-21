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
	    parameters {
		string(name: 'TAG_VERSION', defaultValue: '', description: 'THE TAG OF THE CURRENT VERSION')
		string(name: 'DEV_VERSION', defaultValue: '', description: 'THE VERSION OF THE NEXT DEVELOPPEMENT : ex 01.00.000-SNAPSHOT')
	    }	    
	    
        stages {
            stage("IC - Checkout") {
                steps {
                    checkout scm
                    echo "scm = ${scm}"
                    echo "scm = ${scm.userRemoteConfigs[0].url.replaceAll('https://','')}"
		    echo "env.BRANCH_NAME = ${env.BRANCH_NAME}"
			echo "env.BRANCH_NAME == ~/master/"
               }
            }
            stage("IC - Clean Install") {
		    when {
			// check if branch is master
                        expression {
                            env.BRANCH_NAME == ~/master/
                        }
		    }
                steps {
                     script {
                      //bat 'mvn -Dmaven.test.failure.ignore=true install'
                    //bat 'mvn  -Dmaven.test.skip=truet  versions:set  -DgenerateBackupPoms=false -DnewVersion=${params.TAG_VERSION}'
                    //bat "mvn -X -Dmaven.javadoc.skip=true --batch-mode release:clean release:prepare release:perform"
                    //bat 'git add .'
                    //bat 'git commit -m "Test."'
                    bat "git tag -a v${params.TAG_VERSION} -m \"Test Tag.\""
                    bat 'git tag'
                    bat 'git remote show origin'
                    bat "git config --global user.email 'ludovic.brule@gmail.com'"
                    bat "git config --global user.name 'ludovic.brule@gmail.com'"
                    //bat 'git config --global --unset https.proxy'
                    //bat 'git config --global --unset http.proxy'
                    //bat "git push origin v${params.TAG_VERSION}"
                    
                    withCredentials([usernamePassword(credentialsId: '01fdcf13-8f12-47be-9a79-2e2f7a0846d0', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                      //  bat "echo 'GIT_USERNAME = ${GIT_USERNAME}'>ludo.txt"
                       // bat "echo 'GIT_PASSWORD = ${GIT_PASSWORD}'>>ludo.txt"
                        bat "git rebase origin/master"
                        bat "git push -v origin v${params.TAG_VERSION}"
                    }
                }
            }
       }
        }

}
 
