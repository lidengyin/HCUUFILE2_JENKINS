pipeline{
    agent any
    stages {
        stage('Build'){
            steps{
                sh 'export BUILD_ID=dontKillMe'
                sh 'source /etc/profile'
                sh '''
                ps -ef | grep /var/lib/jenkins/workspace/HCUUFILE_JENKINS_2/target/hcuufile-0.0.1-SNAPSHOT.jar | grep -v grep | awk '{print $2}' | xargs kill -9'
                '''
                sh 'mvn clean package spring-boot:repackage'
           
                 withEnv(['JENKINS_NODE_COOKIE=dontkillme']) {
                        sh """
                             nohup java -Dhudson.util.ProcessTree.disable=true -jar /var/lib/jenkins/workspace/HCUUFILE_JENKINS_2/target/hcuufile-0.0.1-SNAPSHOT.jar > output 2>&1 &
                        """
                 }
            }
        }
    }
}
