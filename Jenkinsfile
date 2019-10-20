 node {        
        stage("IC - Checkout") {
            checkout scm
        }
        stage("IC - Clean Install") {
            sh 'mvn -Dmaven.test.failure.ignore=true install'
        }
  }
