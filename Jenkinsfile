pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Deploy') {
      steps {
        sh '''echo "start deploy script"
BUILD_ID=dontKillMe nohup java -jar target/cap-java.jar &
echo $(ps -ef|grep java)
echo "deploy script end"'''
      }
    }
  }
}
