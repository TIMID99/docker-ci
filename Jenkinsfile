node {
    stage('Clone repository'){
        git credentialsId: 'git-access', url: 'https://github.com/TIMID99/docker-ci.git'
    }
    
    stage('Run lint and build'){
        sh 'npm install'
        sh 'npm run lint'
        sh 'npm run build'
    }

    stage('Serve and Test'){
        sh 'npm run serve &'
        sh 'sleep 60'
        sh '''
        if curl -I http://localhost:8081; then
            echo "Frontend server is running successfully.";
            pkill -f "npm run serve";
        else
            echo "Error: Frontend server failed to start." >&2;
            pkill -f "npm run serve";
            exit 1;
        fi
        '''
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
