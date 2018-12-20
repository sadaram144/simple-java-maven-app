<<<<<<< HEAD
@Library('kp-library@rel_1.1.0') _

buildDeploy(
emailRecipients: "Gangadhar.Sadaram@kp.org",
unitArchiveOnly: true,
disableCodeAnalysis: true,
disableUnit: true,
)
=======
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
>>>>>>> fbd42ca21cafa416fb0f178af668399a1aaa9bb6
