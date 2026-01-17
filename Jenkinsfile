
pipeline {
    agent any
    
    triggers {
        githubPush()
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Maven Build') {
            steps {
                sh '''
                    mvn -version
                    mvn clean package -DskipTests
                '''
            }
        }

        stage(' Docker compose') {
            steps {
                    sh '''
  docker compose down --volumes --remove-orphans || true
  docker system prune -f
  docker compose up -d --build

                '''
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}
