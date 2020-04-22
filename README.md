# Kubernetes + Jenkins demo

This showcase aims to demonstrate the ease of use of Kubernetes pipelines within Jenkins.

Assuming you already have a Jenkins pipeline using the Docker executor, all you need is :

  - a standard Jenkinsfile using the Kubernetes provider instead of Docker
  - a YAML definition of your build pod (build-pod.yaml)