node {
    stage('Checkout') {
        git url: 'https://github.com/dbwjd8653-a11y/jekins.git', branch: 'main', credentialsId: 'github-checkout-token'
    }

    stage('Build') {
        try {
            bat 'npm install'
            bat 'npm run build'
        } catch (e) {
            error "빌드 실패: ${e}"
        }
    }
}