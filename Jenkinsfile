pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Set Up Python Environment') {
            steps {
                bat '''
                    python -m venv venv
                    call venv\\Scripts\\activate
                    python -m pip install --upgrade pip
                    python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Run pytest') {
            steps {
                bat '''
                    call venv\\Scripts\\activate
                    python -m pytest tests/ --junitxml=pytest-report.xml
                '''
            }
        }
    }

    post {
        always {
            junit 'pytest-report.xml'
        }
        success {
            echo '테스트 자동화가 성공적으로 완료되었습니다!'
        }
        failure {
            echo '테스트 자동화 중 일부 테스트가 실패했습니다. 리포트를 확인해주세요.'
        }
    }
}