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
          steps{
deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://54.226.54.3:8080')], contextPath: 'myapp', war: 'target/*.war'
            }
        }
      }        
}
        
