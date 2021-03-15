pipeline {
  agent {
    kubernetes {
      label 'helloworld-app'  // all your pods will be named with this prefix, followed by a unique id
      idleMinutes 5  // how long the pod will live after no jobs have run on it
      yamlFile 'build-pod.yml'  // path to the pod definition relative to the root of our project 
      defaultContainer 'maven'  // define a default container if more than a few stages use it, will default to jnlp container
    }
  }
  stages {
    stage('Build') {
      steps {  // no container directive is needed as the maven container is the default
        sh "mvn clean package"
      }
    }
    stage('Build Docker Image') {
      steps {
        container('docker') {
          withCredentials([[$class: 'UsernamePasswordMultiBinding',
            credentialsId: 'dockerhub',
            usernameVariable: 'DOCKER_HUB_USER',
            passwordVariable: 'DOCKER_HUB_PASSWORD']]) {
              sh """
                docker login -u ${DOCKER_HUB_USER} -p ${DOCKER_HUB_PASSWORD}
                docker build -t harbor.kube.pic.local/k8s-jenkins-demo/helloworld-app:latest .
                docker push harbor.kube.pic.local/k8s-jenkins-demo/helloworld-app:latest
              """
        }
      }
    }
  }
}
