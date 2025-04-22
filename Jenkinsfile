pipeline {
   agent any
   environment {
       SONAR_TOKEN = credentials('sonar-token')
       DOCKER_HUB_USER = credentials('dockerhub-username')
       DOCKER_HUB_PASS = credentials('dockerhub-password')
   }
   tools {
       nodejs 'NodeJS 18'
       python 'Python 3.10'
   }
   stages {
       stage('Checkout') {
           steps {
               git 'https://github.com/Maina-M/Full-Stack-CRUD-API.git'
           }
       }
       stage('Backend Setup') {
           steps {
               dir('backend') {
                   sh 'pip install poetry'
                   sh 'poetry install'
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
               sh 'docker build -t yourdockerhub/fullstack-backend ./backend'
               sh 'docker build -t yourdockerhub/fullstack-frontend ./frontend'
           }
       }
       stage('Deploy via Ansible') {
           steps {
               sh 'wsl ansible-playbook ansible/deploy.yml'
           }
       }
   }
}