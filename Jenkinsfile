pipeline {
    agent any

    tools {
        nodejs "node20"
    }


    environment {
        DOCKER_IMAGE = "my-react-app:${env.BUILD_ID}"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing npm packages...'
                sh 'npm install'
            }
        }

        stage('Build Static Assets') {
            steps {
                echo 'Running npm run build...'
                sh 'npm run build'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${DOCKER_IMAGE} -f NginxDockerfile ."
            }
        }
    }

    post {
        success {
            echo "Successfully built: ${DOCKER_IMAGE}"
        }
        failure {
            echo "Build failed. Check the console output."
        }
    }
}
