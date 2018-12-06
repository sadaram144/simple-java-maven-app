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
                 def server = Artifactory.server 'Art -1'
                 def rtMaven = Artifactory.newMavenBuild() 
                 echo 'Testing 1'          
                 def uploadSpec = """{
                    "files": [{
                       "pattern": "com.mycompany.app/my-app/1.0-SNAPSHOT/my-app-1.0-SNAPSHOT.jar/",
                       "target": "libs-snapshot-local/",
                        "regexp": "true"
                    }]
                 }"""
                def buildInfo = Artifactory.newBuildInfo()
                server.upload spec: uploadSpec, buildInfo: buildInfo
                server.publishBuildInfo buildInfo  
                // server.upload(uploadSpec) 
               }
            }
        }
    }
}
