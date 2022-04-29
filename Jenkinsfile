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
  stage ('Deploy to Dev') { 
    def dockerRun = 'docker run -d -p 9000:8080 —name my-tomcat-app mohitknamdeo/mohit-app:1.0.0'
    sshagent(['841d7a4e-c9db-4b81-8be4-b1fefcce3fa9']) { 
      sh "ssh -o StrictHostKeyChecking=no root@18.224.181.103 ${dockerRun}"
    }
  } 
}  


