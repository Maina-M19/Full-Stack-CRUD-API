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
                   sh 'pip install --upgrade pip'
                   sh 'pip install poetry'
                   sh 'poetry install --no-root'
               }
           }
       }
       stage('Frontend Setup') {
           steps {
               dir('frontend') {
                   sh 'npm install'
                   sh 'npm run build'
               }
           }
       }
       stage('Run Backend Tests') {
           steps {
               dir('backend') {
                   sh 'pytest --cov=app --cov-report=xml:coverage.xml'
               }
           }
       }
       stage('Run Frontend Tests') {
           steps {
               dir('frontend') {
                   sh 'npm run test -- --coverage'
               }
           }
       }
       stage('SonarCloud Analysis') {
           steps {
               withSonarQubeEnv('SonarCloud') {
                   sh 'sonar-scanner'
               }
           }
       }
       stage('Docker Build') {
           steps {
                sh 'docker build -t maina19/fullstack-backend ./backend'
                sh 'docker build -t maina19/fullstack-frontend ./frontend'
            }
        }
       stage('Deploy via Ansible') {
           steps {
               withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_HUB_USER', passwordVariable: 'DOCKER_HUB_PASSWORD')]){
               sh 'wsl ansible-playbook ansible/deploy.yml'
               }
           }
       }
   }
}