
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
                    mvn clean package
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
	stage("docker push"){
      steps{
         script
               {
          // This step should not normally be used in your script. Consult the inline help for details.
withDockerRegistry(credentialsId: '1f864436-96dd-415c-bd9e-16208f04229f', url: 'https://index.docker.io/v1/') {
    sh ''' docker push ajith7353/springcicd:latest '''
}
}
}
}
    }




    post {
        success {
            echo "Pipeline executed successfully"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}
