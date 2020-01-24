pipeline{
    agent any
    stages {
        stage('Build'){
            steps{
             
                sh 'export BUILD_ID=dontKillMe'
                sh 'source /etc/profile'
                PROCESS_ID = sh (script: "ps -ef | grep /var/lib/jenkins/workspace/HCUUFILE_JENKINS_2/target/hcuufile-0.0.1-SNAPSHOT.jar  | grep java | grep jar | grep -v grep | grep -v pipeline | awk -F ' ' '{print \$2}'", returnStdout: true).trim()

echo "PROCESS_ID=" + PROCESS_ID

if (PROCESS_ID != "") {
    sh """
         echo "Kill process: ${PROCESS_ID}"
         sudo kill -9 ${PROCESS_ID}
        """
}
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
