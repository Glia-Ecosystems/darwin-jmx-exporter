pipeline {
  agent none

  tools {
    maven 'Maven_352'
  }

  environment {
    JMX_EXPORTER_RELEASE = 'https://github.com/Glia-Ecosystems/darwin-jmx-exporter/archive/parent-0.12.0.tar.gz'
  }

  stages {
    stage('Initialize') {
      agent any
      
      steps {
        echo "JMX_EXPORTER_RELEASE = ${env.JMX_EXPORTER_RELEASE}"
      }
    }

    stage('Download') {
      agent any

      steps {
        sh """#!/bin/bash
          wget -O exporter.tar.gz ${env.JMX_EXPORTER_RELEASE}
          tar xvfz exporter.tar.gz
        """
      }
    }

    // stage('Build Exporter') {
    //   agent any

    //   steps {
    //     docker_login_ecr()
    //     docker_login_nexus()
    //     remove_docker_networks()

    //     sh '''

    //     '''
    //   }
    // }
  }
}