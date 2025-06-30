pipeline {
    agent any

    environment {
        IMAGE_NAME = "hello-world-image/spring-app"
        IMAGE_TAG = "build-${env.BUILD_NUMBER}"
    }

    
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/amazon7737/hello-world.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building from GitHub!'
                // 예시: 빌드 스크립트 실행 (필요하면 실제 빌드 커맨드로 교체)
                sh './gradlew clean build'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker push ${IMAGE_NAME}:${IMAGE_TAG}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ Docker image pushed: ${IMAGE_NAME}:${IMAGE_TAG}"
        }
        failure {
            echo "❌ Build or push failed."
        }
    }
}
