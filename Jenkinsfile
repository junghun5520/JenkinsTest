pipeline {
    agent any
    environment {
        LANG = 'C.UTF-8'
        LC_ALL = 'C.UTF-8'
    }
    stage('Step 1: 소스 가져오기') {
    steps {
        // 기존에 혹시 남아있을지 모르는 찌꺼기 파일을 싹 지우고 다시 받습니다.
        deleteDir() 
        checkout scm
    }
    }

    stage('Step 2: 웹 서버 실행 (Docker)') {
        steps {
            echo '1. 기존 서버와 안 쓰는 자원 싹 정리'
            sh 'docker rm -f my-web-server || true'
            
            // 안 쓰는 Docker 이미지나 네트워크 찌꺼기를 정리 (선택사항이지만 확실함)
            sh 'docker system prune -f' 

            echo '2. 새로운 Nginx 서버 실행'
            sh 'docker run -d --name my-web-server -p 8081:80 nginx'
            
            echo '3. GitHub에서 갓 가져온 index.html을 서버로 복사'
            // 여기서 ${WORKSPACE}를 명시해서 경로를 확실히 잡습니다.
            sh 'docker cp ${WORKSPACE}/index.html my-web-server:/usr/share/nginx/html/index.html'
        }
    }
        
        stage('Step 3: 배포 완료 확인') {
            steps {
                echo '웹 서버가 성공적으로 실행되었습니다!'
                echo '브라우저에서 http://localhost:8081 에 접속해보세요.'
            }
        }
    }