pipeline {

    agent any

    stages {
        
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/shubhshelke/micro-project.git']]])
            }
        }

        stage('Dokcer Build') {
            steps {
                
                sh 'docker build -t ml_app  .'
               
            }
        }
        
        
    stage('Login') {
        environment { 
                    DOCKERHUB_CREDENTIALS_PSW='dckr_pat_JNAEypaphW_2Vt4Jncj-GXWi_MY'
                    DOCKERHUB_CREDENTIALS_USR='shubhshelke'
                    
                }

      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
           environment { 
               
                    DOCKERHUB_CREDENTIALS_USR='shubhshelke'
                    
                }
      steps {
        sh 'docker push $DOCKERHUB_CREDENTIALS_USR/ml_app:latest'
      }
    }
        
    }
    
}
