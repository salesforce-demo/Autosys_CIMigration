pipeline {
    agent any
    //tools {
      //  maven "localMaven"
       // jdk "Java17"
   // }

environment {
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "20.235.240.119:8081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "demo-java"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "nexus"
        ARTIFACT_VERSION = "${BUILD_NUMBER}"
    }

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
     stage("publish to nexus") {
            steps {
                script {
                    // Read POM xml file using 'readMavenPom' step , this step 'readMavenPom' is included in: https://plugins.jenkins.io/pipeline-utility-steps
                   // pom = readMavenPom file: "pom.xml";
                    // Find built artifact under target folder
                   // filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    // Print some info from the artifact found
                   // echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    // Extract the path from the File found
                  //  artifactPath = filesByGlob[0].path;
                    // Assign to a boolean response verifying If the artifact name exists
                 //   artifactExists = fileExists artifactPath;

                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";

                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: pom.groupId,
                            version: ARTIFACT_VERSION,
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                // Artifact generated such as .jar, .ear and .war files.
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging]
                            ]
                        );

                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }  
       // stage('Nexus artifactory') { 
       //      steps {
       //          echo "This is nexus artifactory stage"
       //          nexusArtifactUploader credentialsId: 'nexus', groupId: 'com.domain', nexusUrl: '20.235.240.119:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://20.235.240.119:8081/#admin/repository/repositories:demo-java', version: '1.0-SNAPSHOT'
       //      }
       //  }
 
 
       // stage('Deploy') { 
         //   steps {
           //     echo "This is my Deployment job"
             //   deploy adapters: [tomcat9(credentialsId: 'TomcatDeployment', path: '', url: 'http://54.163.10.210:8085/')], contextPath: null, war: '**/*.war'
           // }
       // }
    }
}
