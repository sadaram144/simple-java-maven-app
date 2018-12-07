node {
        stage('Build') {
                sh 'mvn -B -DskipTests clean package'
                echo 'Package Build'
        }
        stage('upload') {
                 def server = Artifactory.server('Art -1') 
                 def rtMaven = Artifactory.newMavenBuild()
                 rtMaven.resolver server: server, releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot'
                 rtMaven.deployer server: server, releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local'      
                 echo 'Testing 1'          
                 def uploadSpec = """{
                    "files": [{
                       "pattern": "target/Artifactory-1.0-SNAPSHOT.jar",
                       "target": "libs-snapshot-local/",
                        "regexp": "true"
                    }]
                 }"""
                def buildInfo = Artifactory.newBuildInfo()
                server.upload spec: uploadSpec, buildInfo: buildInfo
                server.publishBuildInfo buildInfo  
                server.upload(uploadSpec) 
        }
    
}
