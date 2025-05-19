pipeline {
    agent any

    tools {
        maven "mymaven"
    }

    environment {
        VERSION = "v1.0.${BUILD_NUMBER}"
    }

    stages {
        stage('code')
        {
            steps{
                git 'https://github.com/EJaishnavi/one.git'
            }
        }
        stage("maven-build") {
            steps {
                sh 'mvn clean package'
            }
        }

        stage("deploy to app server") {
            steps {
                sh 'ls -la target/'
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'mytomcat',
                        path: '',
                        url: 'http://3.86.52.235:8080'
                    )
                ], contextPath: 'zomato', war: 'target/myweb-8.7.3.war'
            }
        }

        stage('Generate Version File') {
            steps {
                script {
                    def versionFile = 'version.txt'
                    writeFile file: versionFile, text: "${env.VERSION}\n"
                    echo "Version written to ${versionFile}: ${env.VERSION}"
                }
            }
        }

        stage('Archive Version File') {
            steps {
                archiveArtifacts artifacts: 'version.txt', fingerprint: true
            }
        }
    }
}
