pipeline {
  agent any
  stages {
    stage('greeting') {
      steps {
        sh '''echo "hello! welcome to compose implementation"
'''
      }
    }
    stage('run test') {
      steps {
        sh '''docker-compose build
        docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)
        docker-compose run web ./scripts/setup.sh rails test
'''
      }
    }
    
    stage('docker clean') {
      steps {
        sh '''
        docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)
        docker system prune -f
'''
      }
    }    
    stage('build image'){
      steps {
        sh '''
        docker build -t rameshmck/jukebox:$BUILD_NUMBER
'''
      }
    }      

    stage('login and push'){
      steps {
        sh '''
        docker login -u rameshmck -p $DOCKER_PASSWORD
        docker build -t rameshmck/jukebox:$BUILD_NUMBER
'''
      }
    }    
    environment {
    DOCKER_PASSWORD = credentials('DOCKER_PASSWORD')
  }
  }
}