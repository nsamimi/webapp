pipeline {
  agent any
  /*
  tools {
    maven 'Maven'
  }
  */
  stages {
    
    stage('Initialize') {
      steps {
        sh '''
          echo "PATH = ${PATH}"
          echo "M2_HOME = ${M2_HOME}"
        '''
      }
    }
    
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    
    stage('Deploy-To-Tomcat') {
      steps {
        sshagent(['master-root-key']) {
          /* 'target/*.war' in Jenkingsfile translates to '/root/.jenkins/workspac     e/webapp-cicd-pipeline/target' */
          sh 'scp -o StrictHostKeyChecking=no target/*.war root@172.17.0.3:/apps/tomcat/webapps/webapp.war'
        }  
      }  
    }  
    
  }
}
