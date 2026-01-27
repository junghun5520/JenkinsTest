pipeline {
    agent any

    stages {
        stage('Step 1: 준비') {
            steps {
                echo 'GitHub로부터 코드를 성공적으로 가져왔습니다!'
                sh 'ls -al'
            }
        }
        stage('Step 2: 검사') {
            steps {
                echo '파일들에 이상이 없는지 체크 중...'
                sh 'cat README.md'
            }
        }
        stage('Step 3: 완료') {
            steps {
                echo '축하합니다! 모든 자동화 공정이 끝났습니다.'
            }
        }
    }
}