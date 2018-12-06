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

    stage('Clone sources') {
        git url: 'https://github.com/sadaram144/simple-java-maven-app.git'
        echo 'mvn version'
    }

    stage('Artifactory configuration') {
    script {         
                 def server = Artifactory.server 'Art -1'
                 def rtMaven = Artifactory.newMavenBuild()   
                 echo 'Testing 1' 
                 
                 rtMaven.resolver server: server, releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot'
                 rtMaven.deployer server: server, releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local'
        
                 def uploadSpec = """{
                    "files": [{
                       "pattern": "com.simple-java-maven-app.app/my-app/1.0-SNAPSHOT/my-app-1.0-SNAPSHOT.jar/",
                       "target": "libs-snapshot-local/",
                        "regexp": "true"
                    }]
                 }"""
                
                def buildInfo = Artifactory.newBuildInfo()
                
                rtMaven.run pom: 'simple-java-maven-app/pom.xml', goals: 'clean install', buildInfo: buildInfo

                server.publishBuildInfo buildInfo                
        
                 server.upload(uploadSpec) 
               }
    }
}

