pipeline {
  agent none

  tools {
    maven 'Maven_352'
  }

  environment {
    JMX_EXPORTER_VERSION = '0.12.0'
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
          wget -O exporter.tar.gz https://github.com/Glia-Ecosystems/darwin-jmx-exporter/archive/parent-${env.JMX_EXPORTER_VERSION}.tar.gz
          mkdir exporter
          tar xvfz exporter.tar.gz -C exporter
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
          cd exporter
          mvn package
        """
      }
    }

    stage('Upload to S3') {
      agent any

      steps {
        s3_upload(
          bucket: "glia-installers-bucket",
          path: "exporter/jmx_exporter-parent-${env.JMX_EXPORTER_RELEASE}/jmx_prometheus_javaagent/target/",
          region: "eu-west-1")
      }
    }
  }
}