node{ 
  stage ('scm checkout') { 
    git 'https://github.com/mohitknamdeo/docker-ci-cd.git'
  }
  stage ('Checkout to different branch') { 
    sh "git branch -r"
    sh "git checkout master"
  } 
  stage ('docker image build') { 
    sh 'docker build . -t mohitknamdeo/mohit-app:1.0.0 '
  } 
  stage ('Push Docker image to DockerHub') { 
    withCredentials([string(credentialsId: 'DockerPass', variable: 'Credential')]) { 
      sh 'docker login -u mohitknamdeo -p ${Credential}'
    } 
    sh 'docker push mohitknamdeo/mohit-app:1.0.0'
  } 
}  


