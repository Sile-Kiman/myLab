pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    // Set Environment :  Moven utilies
        environment{
            GroupId = readMavenPom().getGroupId()
            ArtifactId = readMavenPom().getArtifactId()
            Packaging = readMavenPom().getPackaging()
            Version = readMavenPom().getVersion()
            Name = readMavenPom().getName()

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
        stage ('Pint Environment'){
            steps {
                echo ' testing......'
                echo  "Group Id is.. '${GroupId}'" 
                echo  "Artifact  Id is.. '${ArtifactId}'"
                echo  "Packaging   is.. '${Packaging}'" 
                echo  "Version is.. '${Version}'" 
                echo  "Name is.. '${Name}'"

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
            steps {

                script{
                   def NexusRepo = Version.endsWith("SNAPSHOT") ?  "Sile-KimanDevOpsLab-SNAPSHOT" : "Sile-KimanDevOpsLab-RELEASE"
                 
                 nexusArtifactUploader artifacts: 
                   [artifactId: "${ArtifactId}", 
                   classifier: '', 
                   file: "target/${ArtifactId}-${Version}.war",
                   type: "${Packaging}"], 
                   credentialsId: '7d9cc9b0-01e4-4445-bd12-17604b98cf93', 
                   groupId: "${GroupId}", 
                   nexusUrl: '172.20.10.82:8081', 
                   nexusVersion: 'nexus3', 
                   protocol: 'http', 
                   repository: "${NexusRepo}" , 
                   version: "${Version}" 
                }
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