pipeline {

def server = Artifactory.newServer url: http://localhost:8081/artifactory/, credentialsId: admin,password
def rtMaven = Artifactory.newMavenBuild()
def buildInfo

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

    stages ('Artifactory configuration') {
        rtMaven.tool = MAVEN_TOOL // Tool name from Jenkins configuration
        rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
        rtMaven.resolver releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot', server: server
        buildInfo = Artifactory.newBuildInfo()
    }

    stages ('Exec Maven') {
        rtMaven.run pom: 'simple-java-maven-app/pom.xml', goals: 'clean install', buildInfo: buildInfo
    }

    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }
}
