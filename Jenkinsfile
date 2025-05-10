pipeline {
    agent any

    tools {
        maven 'Maven 3'  // Utilise le nom configuré de Maven dans Jenkins
        jdk 'JDK 17'    // Utilise le nom configuré de JDK 17 dans Jenkins
    }

    environment {
        // Définit le token d'authentification pour SonarQube (à ajouter dans Jenkins)
        SONAR_TOKEN = 'sqa_81545c4de3384ce6513aaba24a77734ec7c294d5'
    }

    stages {
        stage('Clone code') {
            steps {
                git 'https://github.com/utilisateur/sonarqube.git'
            }
        }

        stage('Build') {
            steps {
                // Compile ton projet avec Maven
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    // Analyse ton projet avec SonarQube
                    sh 'mvn sonar:sonar -Dsonar.projectKey=projet-java -Dsonar.host.url=http://localhost:9000 -Dsonar.login=$SONAR_TOKEN'
                }
            }
        }
    }
}
