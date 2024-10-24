pipeline {
  agent any

  environment {
    DOCKER_CREDENTIALS = credentials('DOCKER_ACCOUNT')
  }

  stages {
    stage('build-one') {
      steps {
        echo 'Building'
        sh './gradlew clean build'
      }
    }
    
    stage ('Build-two') {
      steps {
        echo 'Building image...'
        sh 'docker build -t matsandy/spring-gradle:latest .'
      }
    }

    stage ('Run') {
      steps {
        echo 'Running image'
        sh 'docker run -p 8086:8080 -d matsandy/spring-gradle:latest'
      }
    }
    
    stage('login') {
      steps {
        echo 'Connecting to Dockerhub'
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage ('Push') {
      steps {
        echo 'Pushing to Dockerhub'
        sh 'docker push matsandy/spring-gradle:latest'
        }
      }
    }

    post {
      always {
        echo 'PIPELINE FINISHED'
      }
    }
  }
        
        
