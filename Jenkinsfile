node {
    stage('Clone repository'){
        git credentialsId: 'git-access', url: 'https://github.com/TIMID99/docker-ci.git'
    }
    
    stage('Build image'){
        dockerImage = docker.build("meteorwoo99/frontend:1.0")
    }
    
    stage('Push Image') {
        withDockerRegistry([ credentialsId: "docker-access", url: "" ]) {
        dockerImage.push()
        }
    }
}
