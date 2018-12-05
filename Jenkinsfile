pipeline {
    agent {
        docker {
            image 'maven'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
    }
    stages {
        stage('upload') {
           steps {
              script {
                 def server = Artifactory.server 'art-1'
                 def uploadSpec = """{
                    "files": [{
                       "pattern": "path/",
                       "target": "path/"
                    }]
                 }"""
                 server.upload(uploadSpec)
               }
            }
        }
    }
}
