pipeline {
    agent any
    environment {
        ANYPOINT = credentials('ANYPOINT')
    }
    tools {
        maven "maven"
        jdk "jdk11"
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
        stage('Deploy CloudHub to sandbox') { 
        	when {
	          branch 'main'
	      	}
            steps {
                sh "mvn -X clean deploy -DmuleDeploy -Dusername=${ANYPOINT_USR} -Dpassword=${ANYPOINT_PSW} -DappName=testjenkinsapp-sandbox -Denvironment=Sandbox" 
            }
        }
        stage('Deploy CloudHub to test') { 
	        when {
	          branch 'test'
	      	}
            steps {
                sh "mvn -X clean deploy -DmuleDeploy -Dusername=${ANYPOINT_USR} -Dpassword=${ANYPOINT_PSW} -DappName=testjenkinsapp-test -Denvironment=Test" 
            }
        }   
  }
}