pipeline {
   agent any
   environment {
     SERVICE_NAME = "deploytypes"
   }
   stages {
      stage('Preparation') {
         steps {
            git credentialsId: 'GitHub', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }
      stage('Deploy Green OR A version') {
         steps {
            sh 'cat nginx-green.yaml'
            sh 'kubectl apply -f nginx-green.yaml'
         }
      }
      
      stage('Deploy Blue OR B version') {
         steps {
            sh 'cat nginx-blue.yaml'
            sh 'kubectl apply -f nginx-blue.yaml'
         }
      }
      stage('Deploy default or previous version') {
         steps {
            sh 'cat nginx-default.yaml'
            sh 'kubectl apply -f nginx-default.yaml'
         }
      }      
      stage('Configure Routing') {
         steps {
            sh 'cat default-ingress.yaml'
            sh 'kubectl apply -f default-ingress.yaml'
            sh 'kubectl apply -f canary-ingress.yaml'
         }
      }
   }
}
