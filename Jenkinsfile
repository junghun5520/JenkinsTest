pipeline {
    agent any
    environment {
        LANG = 'C.UTF-8'
        LC_ALL = 'C.UTF-8'
    }
    stages {
        stage('Step 1: 소스 가져오기') {
            steps {
                checkout scm
            }
        }
        stage('Step 2: 웹 서버 실행 (Docker)') {
            steps {
                echo '1. 기존 웹 서버 제거'
                sh 'docker rm -f my-web-server || true'
                
                echo '2. 깨끗한 Nginx 서버 실행'
                sh 'docker run -d --name my-web-server -p 8081:80 nginx'
                
                echo '3. 정훈님이 만든 index.html을 서버 안으로 강제 복사'
                // 이 방식은 권한 문제를 원천 차단합니다.
                sh 'docker cp index.html my-web-server:/usr/share/nginx/html/index.html'
                
                echo '4. 서버 권한 정리'
                sh 'docker exec my-web-server chmod 644 /usr/share/nginx/html/index.html'
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