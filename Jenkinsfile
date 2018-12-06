/* pipeline {
    agent any
  
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
                echo 'Package Build'
            }
        }
        stage('upload') {
           steps {
             
                  
                 /*def server = Artifactory.server('Art -1') 
                 def rtMaven = Artifactory.newMavenBuild()
                 rtMaven.resolver server: server, releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot'
                 rtMaven.deployer server: server, releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local'      
                 echo 'Testing 1'          
                 def uploadSpec = """{
                    "files": [{
                       "pattern": "com.simple-java-maven-app.App/my-app/1.0-SNAPSHOT/my-app-1.0-SNAPSHOT.jar/",
                       "target": "libs-snapshot-local/",
                        "regexp": "true"
                    }]
                 }"""
                def buildInfo = Artifactory.newBuildInfo()
                
                rtMaven.run pom: 'simple-java-maven-app/pom.xml', goals: 'clean install', buildInfo: buildInfo

                server.publishBuildInfo buildInfo                
              
            }
        }
    }
}
*/


node {
    // Get Artifactory server instance, defined in the Artifactory Plugin administration page.
    def server = Artifactory.server "Art -1"
    // Create an Artifactory Maven instance.
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo

    stage('Clone sources') {
        git url: 'https://github.com/sadaram144/simple-java-maven-app.git'
        echo 'mvn version'
    }

    stage('Artifactory configuration') {
    script {         
                 def server = Artifactory.server 'Art -1'
                 echo 'Testing 1' 
                 def uploadSpec = """{
                    "files": [{
                       "pattern": "com.mycompany.app/my-app/1.0-SNAPSHOT/my-app-1.0-SNAPSHOT.jar/",
                       "target": "libs-snapshot-local/",
                        "regexp": "true"
                    }]
                 }"""

                 server.upload(uploadSpec) 
               }
    }
}

