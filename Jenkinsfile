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
  }
}