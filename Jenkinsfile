pipeline {
    agent any
    environment {
        ANYPOINT = credentials('ANYPOINT')
    }
    tools { 
        maven maven 
        jdk jdk11
    }
    triggers {
        pollSCM('H/2 * * * *') 
    }
    stages {
        stage('Unit Test') { 
            steps {
                sh "mvn clean install"
            }
        }
        stage('Deploy CloudHub') { 
            steps {
                sh "mvn -X clean deploy -DmuleDeploy -Dusername=${ANYPOINT_USR} -Dpassword=${ANYPOINT_PSW} -DappName=test_jenkins_app -Denvironment=Sandbox" 
            }
        }   
  }
}