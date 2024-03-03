pipeline {
    agent any

    stages {
        stage('Build Docker image') {
            steps {
                script {
                    bat 'docker build -t django-to-do .'
                }
            }
        }
        stage('Tag image') {
            steps {
                script {
                    bat 'docker tag django-to-do carribo/django-to-do'
                }
            }
        }
        stage('Push image') {
            environment {
                DOCKER_HUB_CREDENTIALS = credentials('dockerhub-credentials')
            }
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD']]) {
                    script {
                        bat 'docker logout'
                        bat "docker login -u ${DOCKER_HUB_USERNAME} -p ${DOCKER_HUB_PASSWORD}"
                        bat 'docker push carribo/django-to-do'
                        bat 'echo "Hello"'
                    }
                }
            }
        }
    }
}