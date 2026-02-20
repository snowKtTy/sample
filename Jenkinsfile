pipeline {
    // 파이프라인이 실행될 에이전트를 지정합니다. (any는 사용 가능한 어떤 node든 사용)
    agent any

    // 환경 변수 설정
    environment {
        APP_NAME = "my-awesome-app"
        DEPLOY_ENV = "staging"
    }

    stages {
        stage('Prepare') {
            steps {
                echo '소스 코드를 가져오고 빌드 환경을 준비합니다...'
            }
        }

        stage('Build') {
            tools {
                gradle 'gradle-8.1.1-bin.zip'
                jdk 'JDK21'
            }
            steps {
                echo '컴파일 및 빌드를 시작합니다...'
                sh 'gradle clean bootJar'
            }
        }

        stage('Test') {
            steps {
                echo '유닛 테스트 및 정적 분석을 수행합니다...'
                sh 'echo "Running tests..."'
            }
        }

        stage('Deploy') {
            steps {
                echo "현재 환경: ${env.DEPLOY_ENV}에 배포 중..."
                sh 'echo "Deploying to server..."'
            }
        }
    }

    // 실행 결과(성공/실패)에 따른 후속 조치
    post {
        always {
            echo '작업이 완료되었습니다. 로그를 정리합니다.'
        }
        success {
            echo '✅ 빌드 및 배포 성공!'
        }
        failure {
            echo '❌ 빌드 실패! 담당자에게 알림을 보냅니다.'
        }
    }
}