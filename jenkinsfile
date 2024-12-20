pipeline {
    agent any

    environment {
        SONARQUBE_URL = 'SonarQube' // Nom de ton serveur SonarQube dans Jenkins
    }

    stages {
        // Étape pour Node.js
        stage('Node.js - Build') {
            steps {
                dir('node-app') {
                    echo 'Building Node.js application...'
                    sh 'npm install'
                }
            }
        }
        stage('Node.js - Test') {
            steps {
                dir('node-app') {
                    echo 'Running Node.js tests...'
                    sh 'npm test'
                }
            }
        }

        // Étape pour PHP
        stage('PHP - Build') {
            steps {
                dir('php-app') {
                    echo 'Installing PHP dependencies...'
                    sh 'composer install'
                }
            }
        }
        stage('PHP - Test') {
            steps {
                dir('php-app') {
                    echo 'Running PHP tests...'
                    sh './vendor/bin/phpunit'
                }
            }
        }

        // SonarQube Analysis pour les deux projets
        stage('SonarQube Analysis') {
            steps {
                echo 'Running SonarQube analysis...'
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner -Dsonar.projectKey=projet-ci-cd'
                }
            }
        }

        // Déploiement (Exemple)
        stage('Deploy') {
            steps {
                echo 'Deploying applications...'
                sh 'echo "Deployment complete for Node.js and PHP!"'
            }
        }
    }
}
