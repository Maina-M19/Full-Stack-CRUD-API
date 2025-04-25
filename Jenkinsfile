pipeline {
   agent any
   environment {
       SONAR_TOKEN = credentials('sonar-token')
   }
   tools {
       nodejs 'NodeJS 18'
   }
   stages {
       stage('Checkout') {
           steps {
               git 'https://github.com/Maina-M19/Full-Stack-CRUD-API.git'
           }
       }
       stage('Backend Setup') {
           steps {
               dir('backend') {
                   bat 'pip install --upgrade pip'
                   bat 'pip install poetry'
                   bat 'poetry lock'
                   bat 'poetry install'
               }
           }
       }
       stage('Frontend Setup') {
           steps {
               dir('frontend') {
                   bat '''set NODE_OPTIONS=--max_old_space_size=4096
                   npm install
                   npm run build
                   '''
               }
           }
       }
       stage('SonarCloud Analysis') {
           steps {
               script{
                   def scannerHome = tool 'SonarScanner'
                   withSonarQubeEnv('SonarCloud') {
                        bat 'set _JAVA_OPTIONS=-Xmx1024m && ' + "${scannerHome}\\bin\\sonar-scanner"   
                   }
               }
           }
       }
       stage('Docker Build') {
           steps {
                    bat 'docker build -t maina19/fullstack-backend ./backend'
                    bat 'docker build -t maina19/fullstack-frontend ./frontend'
                }
       }
       stage('Deploy via Ansible') {
           steps {
               withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_HUB_USER', passwordVariable: 'DOCKER_HUB_PASSWORD')]){
               bat ''' 
               wsl -d Ubuntu ansible-playbook /mnt/c/Users/techm/.jenkins/workspace/test/ansible/deploy.yml \
               -e "docker_username=%DOCKER_HUB_USER% docker_password=%DOCKER_HUB_PASSWORD%"
               '''
            }
        }
    }
   }
}