pipeline {
    agent any

    environment {
        VENV_DIR = "${WORKSPACE}/venv"
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📦 GitHub에서 소스 코드를 가져옵니다...'
                git credentialsId: 'your-ssh-key-id', url: 'git@github.com:HALOYOSHI/your-python-project.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo '🔧 가상환경을 생성하고 의존성을 설치합니다...'
                sh '''
                    python3 -m venv ${VENV_DIR}
                    source ${VENV_DIR}/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo '🧪 테스트를 실행합니다...'
                sh '''
                    source ${VENV_DIR}/bin/activate
                    pytest --maxfail=1 --disable-warnings -v
                '''
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo '🚀 (선택 사항) 배포 작업을 실행합니다...'
                // 배포 스크립트 삽입 가능
                // 예: scp, rsync, Docker push, etc.
            }
        }
    }

    post {
        success {
            echo '✅ 파이프라인이 성공적으로 완료되었습니다.'
        }
        failure {
            echo '❌ 파이프라인 실패. 로그를 확인하세요.'
        }
    }
}
