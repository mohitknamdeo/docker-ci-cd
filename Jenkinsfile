node{ 
  stage ('scm checkout') { 
    git 'https://github.com/mohitknamdeo/docker-ci-cd.git'
  }
  stage ('Checkout to different branch') { 
    sh "git branch -r"
    sh "git checkout master"
  } 
  stage ('docker image build') { 
    sh 'docker build . -t mohitknamdeo/mkn-app:1.0.0 '
  } 
  stage ('Push Docker image to DockerHub') { 
    withDockerRegistry([credentialsId: 'mycreds', url: 'https://index.docker.io/v1/' ]) { 
      sh 'docker push mohitknamdeo/mkn-app:1.0.0'
    } 
  } 
  stage ('Deploy to Dev') { 
    sh 'docker run -d -p 9000:8080 --name my-mkn-app mohitknamdeo/mohit-app:1.0.0'
  } 
}  


