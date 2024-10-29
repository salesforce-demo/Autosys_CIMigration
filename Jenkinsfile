pipeline {
    agent any     
       stages {
         stage('GITHUB') { 
            steps {
                echo "This is my SCM Job"
                git 'https://github.com/DineshKuswah/demo-java.git'
            }
        }
         stage('Build and Package') { 
            steps {
                echo "This is my Build Job"
                sh label: '', script: 'mvn clean package'
            }
        }
         stage('Test') { 
             steps {
                 echo "This is my Test job"
             }
         }
       // stage('Nexus artifactory') { 
       //      steps {
       //          echo "This is nexus artifactory stage"
       //          nexusArtifactUploader credentialsId: 'nexus', groupId: 'com.domain', nexusUrl: '20.235.240.119:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://20.235.240.119:8081/#admin/repository/repositories:demo-java', version: '1.0-SNAPSHOT'
       //      }
       //  }
 
 
        stage('Deploy') { 
            steps {
                echo "This is my Deployment job"
                deploy adapters: [tomcat9(credentialsId: 'TomcatDeployment', path: '', url: 'http://54.163.10.210:8085/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}

