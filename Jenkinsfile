pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    // Set Environment :  Moven utilies
        Environment{
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
        stage ('Test'){
            steps {
                echo ' testing......'
                echo "Group Id is.." ${GroupId } 
                echo  "Artifact  Id is.." ${ArtifactId} 
                echo  "Packaging   is.." ${Packaging} 
                echo  "Version is.." ${Version} 
                echo  "Name is.." ${Name} 

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
                 nexusArtifactUploader artifacts: [[artifactId: 'Sile-KimanDevOpsLab', classifier: '', file: 'target/Sile-KimanDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: '7d9cc9b0-01e4-4445-bd12-17604b98cf93', groupId: 'com.Sile-Kimandevopslab', nexusUrl: '172.20.10.82:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Sile-KimanDevOpsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT' 
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