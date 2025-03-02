
pipeline {
   agent any


   stages {
       stage('Code Quality') {
           steps {
               echo 'Sonar Analysis Started perform'
               sh 'cd frontend && sudo docker run --rm -e SONAR_HOST_URL="http://99.79.33.138:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqp_04663fbb1bd020d39f71b30e29155344fac5ebc1" sonarsource/sonar-scanner-cli -Dsonar.projectKey=chat-app'
               echo 'Sonar Analysis Completed'
           }
       }
   }
}