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
                   bat 'poetry install --no-root'
               }
           }
       }
       stage('Frontend Setup') {
           steps {
               dir('frontend') {
                   bat 'npm install'
                   bat 'npm run build'
               }
           }
       }
       stage('Run Backend Tests') {
           steps {
               dir('backend') {
                   bat 'pytest --cov=app --cov-report=xml:coverage.xml'
               }
           }
       }
       stage('Run Frontend Tests') {
           steps {
               dir('frontend') {
                   bat 'npm run test -- --coverage'
               }
           }
       }
       stage('SonarCloud Analysis') {
           steps {
               script{
                   def scannerHome = tool 'SonarScanner'
                   withSonarQubeEnv('SonarCloud') {
                   bat "${scannerHome}\\bin\\sonar-scanner"
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
               bat 'wsl ansible-playbook ansible/deploy.yml'
               }
           }
       }
   }
}