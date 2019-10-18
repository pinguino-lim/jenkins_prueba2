pipeline {
    agent {
        docker {
            image 'node:12.4-alpine'
			args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
		USERNAME = credentials('USERNAME')
		ID_PASSWORD = credentials('ID_PASSWORD')
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
		stage('Deploy') {
            steps {
                sh './scripts/deploy.sh' 
				input message: 'Has acabaddo de ver el server? (Click "Processed" para continuar)'
				sh './scripts/kill.sh'
            }
        }
    }
}
