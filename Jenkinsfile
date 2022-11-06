pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages {
        stage('clone repo an ') {
            steps {
                sh 'rm -rf my-app'
                sh 'git clone https://github.com/nihatsayar/my-app.git '
                sh 'mvn clean -f my-app'
            }
        }
        stage('Build') {
            steps {
                sh script 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test -f my-app'
            }
        }
        stage('Upload War To Nexus') {
            steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'my-app',
                        classifier: '',
                        file: 'target/my-app-1.0-SNAPSHOT.war', 
                        type: 'war'
                    ]
               ],
               credentialsId: 'NEXUS_ID',
               groupId: 'com.mycompany.app', 
               nexusUrl: '192.168.116.3:8081',
               nexusVersion: 'nexus2',
               protocol:'http',
               repository: 'maven-repository',
               version: '1.0-SNAPSHOT'
            }
        }
    }
}
