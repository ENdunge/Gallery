pipeline {
  agent any
    
  tools {nodejs "NodeJS"}
    
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
        bat 'heroku rake db:migrate db:seed --app gallery-gal'
      }
    }
  }
}