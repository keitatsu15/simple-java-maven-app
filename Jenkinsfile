pipeline {
    agent any
    tools { maven 'maven3' }

    options {
        timestamps()
        timeout(time: 10, unit: 'MINUTES')
    }

    stages {
        stage('Checkout') {
            steps {
                echo "ブランチ: ${env.BRANCH_NAME ?: 'master'}"
                sh 'git log --oneline -1'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
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
        success {
            echo 'ビルド成功'
        }
        failure {
            echo 'ビルド失敗'
        }
    }
}
