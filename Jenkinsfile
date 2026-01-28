pipeline {
    agent any

    environment {
        LANG = 'C.UTF-8'
        LC_ALL = 'C.UTF-8'
    }

    stages {
        stage('Step 1: 소스 가져오기') {
            steps {
                deleteDir()
                checkout scm
                // 파일이 정말 영어로 바뀌었는지 로그에서 확인해봅시다
                sh 'cat index.html'
            }
        }

        stage('Step 2: 웹 서버 실행 (Docker)') {
            steps {
                echo '기존 서버 제거...'
                sh 'docker rm -f my-web-server || true'
                
                echo '새로운 Nginx 서버 실행...'
                sh 'docker run -d --name my-web-server -p 8081:80 nginx'
                
                echo '파일 복사...'
                sh 'docker cp index.html my-web-server:/usr/share/nginx/html/index.html'
            }
        }

        stage('Step 3: 확인') {
            steps {
                echo '배포가 완료되었습니다! http://localhost:8081 접속 확인'
            }
        }
    }
}