pipeline {
  agent any
    
  tools {nodejs "NodeJS"}

  environment {
        EMAIL_TO = 'n.manguu@gmail.com'
    }
    
  stages {
        
    stage('Git') {
      steps {
        git 'https://github.com/ENdunge/Gallery.git'
      }
    }
     
    stage('Build') {
      steps {
        bat 'npm install'
      }
    }  
    
            
    stage('Test') {
      steps {
        bat 'npm test'
      }
    }

    stage('Deploy') {
      steps {
        bat 'curl "https://api.render.com/deploy/srv-cgjd34mbb6mo06m8sv10?key=tkwMojDaN14" --ssl-no-revoke'
      }
    }
  }

  post {
        always{
            slackSend( channel: "#gallery", token: "slack_webhook token", color: "good", message: "Email from Jenkinsfile")
        }

        failure {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                    to: "${EMAIL_TO}", 
                    subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        unstable {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                    to: "${EMAIL_TO}", 
                    subject: 'Unstable build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        changed {
            emailext body: 'Check console output at $BUILD_URL to view the results.', 
                    to: "${EMAIL_TO}", 
                    subject: 'Jenkins build is back to normal: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    }
}