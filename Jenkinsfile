pipeline {
    agent any

    stages {
        stage('Code Quality') {
            steps {
                echo 'Sonar Analysis Started'

                sh '''cd frontend
                    sudo docker run --rm \
                    -e SONAR_HOST_URL="http://18.231.121.133:9000" \
                    -e SONAR_LOGIN="sqp_f5a4c7be5f497a394fc3fd2ace35bbb12134f7cf" \
                    -v "$(pwd):/usr/src" sonarsource/sonar-scanner-cli:5.0 \
                    -Dsonar.projectKey=chat-app
                '''

                echo 'Sonar Analysis Completed'
            }
        }
    stage('Build chat-app') {
           steps {
               echo 'chat-app Build Started'
               sh 'cd frontend && npm install && npm run build'
               echo 'chat-app Build Completed'
           }
       }
      
       stage('Publish Chat-app') {
           steps {
               script {
                   def packageJson = readJSON file: 'frontend/package.json'
                   def packageJSONVersion = packageJson.version
                   echo "${packageJSONVersion}"
                   sh "zip frontend/chat-app-${packageJSONVersion}.zip -r frontend/dist"
                   sh "curl -v -u admin:wasim123 --upload-file frontend/chat-app-${packageJSONVersion}.zip http://18.231.121.133:8081/repository/chat-app/"
               }
           }
       }
      
       stage('Deploy LMS') {
           steps {
               script {
                   def packageJson = readJSON file: 'frontend/package.json'
                   def packageJSONVersion = packageJson.version
                   echo "${packageJSONVersion}"
                   sh "curl -u admin:wasim123 -X GET \'http://18.231.121.133:8081/repository/chat-app/chat-app-${packageJSONVersion}.zip\' --output chat-app-'${packageJSONVersion}'.zip"
                   sh 'sudo rm -rf /var/www/html/*'
                   sh "sudo unzip -o chat-app-'${packageJSONVersion}'.zip"
                   sh "sudo cp -r frontend/dist/* /var/www/html"
               }
           }
       }
   }
}