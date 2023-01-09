pipeline {
  //agent any
  //agent {label 'master'}
  agent {
        label 'master1'
    }
    stages { 
      //stage('clone') {
        //steps {
          //git branch: 'main', credentialsId: 'github-tocken', url: 'https://github.com/DevOpsSecOps1/MicroService.git'
          //echo 'Clone is susscessful from github'
        //}
      //}
      stage('build') {
       agent {
        label 'master1'
       }
        steps {
          sh "mvn clean package"
          echo 'Build is suscess using maven'
        }
      }
      stage('Test') {
        agent {
        label 'master1'
        }
        steps {
          sh "mvn test"
          echo 'Test cases executed successfully'
        }
      }
      stage('Deployment') {
        steps {
          sshagent(['Deployment_54.88.196.251']) {
          sh """
          scp -rp /home/ec2-user/.jenkins/workspace/Deployment_Job/target/*.jar ec2-user@54.88.196.251:/opt/apache-tomcat-8.5.84/webapps
          ssh ec2-user@54.88.196.251 /opt/apache-tomcat-8.5.84/bin/shutdown.sh
          ssh ec2-user@54.88.196.251 /opt/apache-tomcat-8.5.84/bin/startup.sh
          """
          }
        }
      }
    }
}
