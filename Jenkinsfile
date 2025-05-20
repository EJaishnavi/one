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

stage('Tag Release') {
    steps {
        script {
            def tagName = "v${env.BUILD_NUMBER}" // or use a custom version
             withCredentials([usernamePassword(credentialsId: 'githubcrdentails', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                sh """
                    git config user.email "jenkins@example.com"
                    git config user.name "Jenkins CI"
                    git remote set-url origin https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/EJaishnavi/one.git
                    git tag -a ${tagName} -m "Tagging release ${tagName}"
                    git push origin ${tagName}
                """
            }
        }
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
