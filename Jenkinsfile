
pipeline {
    agent {
        label 'playwright'
    }

    options {
        timestamps()
        skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'node --version'
                sh 'npm --version'
                sh 'npm ci'
            }
        }

        stage('Unit Test - Jest') {
            steps {
                sh 'npm test -- --ci'
            }
        }

        stage('Build Next.js') {
            steps {
                sh 'npm run build'
            }
        }

        stage('E2E Test - Playwright') {
            steps {
                sh 'npx playwright install chromium'
                sh 'npm run test:e2e'
            }
        }
    }

    post {
        always {
            echo 'Pipeline selesai dijalankan.'
        }
        success {
            echo 'CI/CD berhasil!'
        }
        failure {
            echo 'CI/CD gagal. Periksa log setiap stage.'
        }
    }
}
