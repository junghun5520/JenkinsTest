pipeline {
    agent any
    stages {
        stage('Step 1: 소스 가져오기') {
            steps {
                checkout scm
            }
        }
        stage('Step 2: 웹 서버 실행 (Docker)') {
            steps {
                echo '기존 웹 서버가 있다면 끄고, 새로 실행합니다...'
                // 기존에 돌고 있는 nginx가 있으면 끄고 새로 띄우는 명령어입니다.
                sh 'docker rm -f my-web-server || true'
                sh 'docker run -d --name my-web-server -p 8081:80 -v $(pwd):/usr/share/nginx/html nginx'
            }
        }
        stage('Step 3: 배포 완료 확인') {
            steps {
                echo '웹 서버가 성공적으로 실행되었습니다!'
                echo '브라우저에서 http://localhost:8081 에 접속해보세요.'
            }
        }
    }
}