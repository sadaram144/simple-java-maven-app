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
                  def server = Artifactory.server "artifactory@ibsrv02"
                  def buildInfo = Artifactory.newBuildInfo()
                  buildInfo.env.capture = true
                  def rtMaven = Artifactory.newMavenBuild()
                  rtMaven.tool = MAVEN_TOOL // Tool name from Jenkins configuration
                  rtMaven.opts = "-Denv=dev"
                  rtMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
                  rtMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server

                  rtMaven.run pom: 'simple-java-maven-app/pom.xml', goals: 'clean install', buildInfo: buildInfo

                  buildInfo.retention maxBuilds: 10, maxDays: 7, deleteBuildArtifacts: true
                  // Publish build info.
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
                server.upload spec: uploadSpec, buildInfo: buildInfo
                server.publishBuildInfo buildInfo  
                server.upload(uploadSpec) */
               }
            }
        }
    }
}
