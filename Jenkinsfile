currentBuild.displayName = "examplemd#"+currentBuild.number
pipeline{
    agent any
    
    environment{
        PATH = "/opt/maven/bin:$PATH"
    }
    stages{
        stage("git checokeout"){
            steps{
               git 'https://github.com/Baratnannaka/nexus-jenkins.git' 
            }
        }
        stage("mvn build"){
            steps{
                sh "mvn clean package"
                  
            }
        }
        stage("copy to nexus"){
            steps{
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: 'target/simple-app-2.0.0.war', 
                        type: 'war'
                    ]
                ], 
                        credentialsId: 'nexus', 
                        groupId: 'in.javahome', 
                        nexusUrl: '172.31.19.219:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'simple-app', 
                        version: '2.0.0'
            }
        }
    }
}
