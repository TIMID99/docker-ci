pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Clone repository') {
            steps {
                git credentialsId: 'git_access', url: 'https://github.com/TIMID99/docker-ci.git'
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -t meteorwoo99/web_count:1.0 .'
            }
        }
        stage('Push Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-access', url: '']) {
                    sh 'docker push meteorwoo99/web_count:1.0'
                }
            }
        }
    }
}
