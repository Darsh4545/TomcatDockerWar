pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh " /opt/apache-maven-3.9.6/bin compile"
               }
          }
          stage("Unit test") {
               steps {
                    sh " /opt/apache-maven-3.9.6/bin test"
               }
          }
     
    
stage("Package") {
     steps {
          sh " /opt/apache-maven-3.9.6/bin package"
     }
}
stage("Docker build") {
     steps {
      
          sh "docker build -t darshan_tomcat ."
     }
}

stage("Deploy to staging") {
     steps {
          
          sh "docker stop \$(docker ps -qa)"
          sh "docker rm \$(docker ps -qa)"
          sh "docker run -d -it -v /var/lib/jenkins/workspace/pipelne-with-docker/target/:/usr/local/tomcat/webapps/ -p 8091:8080 --name Testtomcat darshan_tomcat"
     }
}

     }
  post {
     always {
          sh "echo 'I did It'"
     }
}
}
