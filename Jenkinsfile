node {
  stage('Checkout') {
    // Use the Git plugin to checkout the code
    git branch: 'master', url: 'https://github.com/Aquilero/jenkins-react-app.git'
  }
  stage('Build') {
    sh 'docker ps --filter name=node | grep node && docker kill node || true'
    sh 'docker run -d --rm --name node -v ${WORKSPACE}:/var/app -w /var/app node:lts-bullseye tail -f /dev/null'
    sh 'docker exec node npm --version'
    sh 'docker exec node ls -la'
    sh 'docker exec node npm ci'
    sh 'echo "YOUR COMMANDS HERE!"'
    sh 'docker exec node npm run build'
    sh 'docker build -t jenkins-react-app:latest .'
    sh 'docker kill node'
  }
    stage('Docker-Image') {
    sh 'docker run -d -p 80:80 jenkins-react-app '
  }
  stage('Cleanup') {
    // Use the Git plugin to checkout the code
    git branch: 'master', url: 'https://github.com/Aquilero/jenkins-react-app.git'
    deleteDir()
  }
}
