pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Deploy-14') {
      steps {
        sh '''echo "start deploy script"
echo "start kill cap-java"
echo `ps aux | grep -v grep | grep \'cap-java\'|awk \'NR==1\'`
pid=`ps aux | grep -v grep | grep "cap-java"|awk \'NR==1 {print $2}\'`
if [ ! $pid ]
then
 echo "no cap-java pid alive"
else
    kill -9 $pid
fi
echo "kill $pid success"
OLD_BUILD_ID=$BUILD_ID
echo $OLD_BUILD_ID
BUILD_ID=DONTKILLME nohup java -jar /home/newdisk/data/jenkins/workspace/Capistrano-java_master/target/cap-java.jar &
sleep 10
echo $(ps -ef|grep java)
echo "deploy script end"'''
      }
    }
    stage('Deploy Groups') {
      steps {
        ansiblePlaybook(playbook: '/home/newdisk/tools/script/java_deploy.yml')
      }
    }
  }
}