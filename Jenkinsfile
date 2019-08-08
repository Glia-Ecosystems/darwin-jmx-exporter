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

    stage('Build Exporter') {
      agent {
        docker {
            image '546056091706.dkr.ecr.eu-west-1.amazonaws.com/dockermvn'
            args '--entrypoint ""'
        }
      }
      steps {
        sh """#!/bin/bash
          cd darwin-jmx-exporter-parent-0.12.0
          mvn package
        """
      }
    }
  }
}