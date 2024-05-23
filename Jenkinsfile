node {
    stage('Clone repository'){
        git credentialsId: 'git_access', url: 'https://github.com/TIMID99/docker-ci.git'
    }
    
    stage('Build image'){
        dockerImage = docker.build("meteorwoo99/web_count:1.0")
    }
    
    stage('Push Image') {
        withDockerRegistry([ credentialsId: "docker-access", url: "" ]) {
        dockerImage.push()
        }
    }
}
