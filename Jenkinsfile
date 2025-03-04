
pipeline {
   agent any


   stages {
       stage('Code Quality') {
           steps {
               echo 'Sonar Analysis Started perform'
               sh 'cd frontend && sudo docker run  --rm -e SONAR_HOST_URL="http://18.231.121.133:9000" -e SONAR_LOGIN="sqp_f5a4c7be5f497a394fc3fd2ace35bbb12134f7cf"  -v ".:/usr/src" sonarsource/sonar-scanner-cli:5.0 -Dsonar.projectKey=chat-app
               echo 'Sonar Analysis Completed'
           }
       }
   }
}