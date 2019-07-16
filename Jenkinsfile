pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B verify'
            }
        }
        stage('test') {
            steps {
                sh "mvn -B test"
            }
        }
        stage('deploy to nexus') {
            steps {
                nexusArtifactUploader(
                        nexusVersion: 'nexus2',
                        protocol: 'http',
                        nexusUrl: '172.21.0.3:8081',
                        groupId: 'org.springframework.samples',
                        version: '2.1.0.BUILD-SNAPSHOT',
                        repository: 'pets',
                        credentialsId: 'deploy_to_nexus',
                        artifacts: [
                                [artifactId: 'spring-petclinic',
                                 classifier: '',
                                 file      : 'target/spring-petclinic-2.1.0.BUILD-SNAPSHOT.jar',
                                 type      : 'jar'
                                ]
                        ]
                )
            }
        }
    }
}
