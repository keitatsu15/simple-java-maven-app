pipeline {
    agent any
    tools { maven 'maven3' }

    stages {
        stage('Test') {
            steps {
                sh 'mvn -B test'
            }
        }
    }
    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
    }
}
