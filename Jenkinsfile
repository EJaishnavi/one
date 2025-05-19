pipeline {
    agent any

    tools {
        maven "mymaven"
    }

    

    stages {
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
                ], contextPath: 'swiggy', war: 'target/*.war'
            }
        }

       

       
    }
}
