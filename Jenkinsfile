#!/usr/bin/env groovy

properties([
  parameters([
    string(defaultValue: 'asia.gcr.io/kubernetes-trial-190502/jenkins-slave', description: '', name: 'JNLP_IMAGE'),
    string(defaultValue: 'jenkins', description: '', name: 'K8S_NAMESPACE'),
  ]),
  pipelineTriggers([])
])

podTemplate(label: 'build-pod',
  containers: [
    containerTemplate(name: 'jnlp', image: JNLP_IMAGE, args: '${computer.jnlpmac} ${computer.name}'),
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
