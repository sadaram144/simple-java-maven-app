pipeline {
   

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
                 def server = Artifactory.newServer url: 'http://localhost:8081/artifactory/', username: 'admin', password: 'password'                 
                 def server = Artifactory.server 'art-1'
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
           
    }
}
