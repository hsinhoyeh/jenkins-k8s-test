#!/usr/bin/env groovy

podTemplate(label: 'build-pod',
  containers: [
    containerTemplate(name: 'jnlp', image: 'asia.gcr.io/axinan-dev/jenkins-slave', args: '${computer.jnlpmac} ${computer.name}'),
    containerTemplate(name: 'golang', image: 'golang:1.9', ttyEnabled: true, command: 'cat')
  ],
  volumes: [
    hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')
  ]
) {
  node('build-pod') {
    container('golang') {
      stage('Checkout') {
          checkout scm
      }

      stage('Prepare') {
        sh """ go version """
      }
    }
  }
}
