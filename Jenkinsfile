pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the source code to Sonarqube
       /** stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                     sh 'mvn sonar:sonar'
                }

            }
        }*/

        //state 3 publish artifacts to Nexus
        stage ('Publish to Nexus'){
            step {
                 nexusArtifactUploader artifacts: [[artifactId: 'Sile-KimanDevOpsLab', classifier: '', file: 'target/Sile-KimanDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: '5801fc57-fe11-475f-b961-2c5c18f5cd87', groupId: 'com.Sile-Kimandevopslab', nexusUrl: '172.20.10.82:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'target', version: '0.0.3-SNAPSHOT'
            }
        }

         // Stage4 : Testing
        stage ('Deploy'){
            steps {
                echo ' deploying......'

            }
        }
        
    }

}