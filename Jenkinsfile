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
                echo '기존 웹 서버 제거...'
                sh 'docker rm -f my-web-server || true'
                
                echo '새로운 웹 서버 실행...'
                // -v 옵션 부분을 아래와 같이 '현재 작업 폴더'를 명확히 가리키도록 수정합니다.
                sh "docker run -d --name my-web-server -p 8081:80 -v ${WORKSPACE}:/usr/share/nginx/html nginx"
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