pipeline {
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
              script {   
                  def server = Artifactory.server "Art -1"
                  def buildInfo = Artifactory.newBuildInfo()
                  buildInfo.env.capture = true
                  def rtMaven = Artifactory.newMavenBuild()
                  rtMaven.tool = "Maven-3.3.9"
                  
                  rtMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
                  rtMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server
                  
                  def uploadSpec = """{
                    "files": [{
                       "pattern": "com.simple-java-maven-app.App/my-app/1.0-SNAPSHOT/my-app-1.0-SNAPSHOT.jar/",
                       "target": "libs-snapshot-local/",
                        "regexp": "true"
                    }]
                 }"""
                  
                  rtMaven.run pom: 'simple-java-maven-app/pom.xml', goals: 'clean install', buildInfo: buildInfo

                  server.publishBuildInfo buildInfo
                  
                  
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
                 */
               }
            }
        }
    }
}
