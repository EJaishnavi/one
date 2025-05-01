pipeline{
agent any
  tools
  {
    maven "mymaven"
  }
stages
  {
    stage("maven-build")
        {
      steps{
sh 'mvn clean package'
}
}
        stage("deploy to app server")
        {
          steps {
            sh 'ls -la target/'
                deploy adapters: [tomcat9(credentialsId: 'mytomcat', path: '', url: 'http://13.218.91.73:8080')], contextPath: 'swiggy', war: 'target/*.war'
            }
        }
      }        
}
