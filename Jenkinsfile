pipeline {
    agent any

    tools {
        maven 'Maven 3'      // Nom configuré de Maven dans Jenkins
        jdk 'JDK 17'         // Nom configuré de JDK 17 dans Jenkins
    }

    environment {
        // Token d'authentification pour SonarQube (doit être configuré dans Jenkins ou injecté via les credentials)
        SONAR_TOKEN = 'sqa_81545c4de3384ce6513aaba24a77734ec7c294d5'
    }

    stages {
        stage('Clone code') {
            steps {
                // Clone du dépôt Git avec les identifiants
                git credentialsId: '22debf94-29e9-4e8a-87ca-963afa903027',
                    url: 'https://github.com/khadijacharafi/sonarqube.git',
                    branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Compilation avec Maven
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    // Analyse SonarQube
                    sh 'mvn sonar:sonar -Dsonar.projectKey=projet-java -Dsonar.host.url=http://localhost:9000 -Dsonar.login=$SONAR_TOKEN'
                }
            }
        }
    }
}
