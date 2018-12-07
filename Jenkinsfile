node {
        stage('Build') {
                sh 'mvn -B -DskipTests clean package'
        }
        stage('upload') {
                 def server = Artifactory.server('Art -1')          
                 def uploadSpec = """{
                    "files": [{
                       "pattern": "target/Artifactory-1.0-SNAPSHOT.jar",
                       "target": "libs-snapshot-local/"                      
                    }]
                 }"""
                def buildInfo = Artifactory.newBuildInfo()
                server.upload spec: uploadSpec, buildInfo: buildInfo
                server.publishBuildInfo buildInfo  
                server.upload(uploadSpec) 
        }
    
}
