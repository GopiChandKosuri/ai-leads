pipeline{
    agent any
    stages{
        stage('code checkout'){
            steps{
                git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/GopiChandKosuri/ai-leads.git'
            }
        }
        stage("Build "){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('tomcat deploy-dev'){
            steps{
                sshagent(['tomcat-dev']){
                    sh " scp -o StrictHostKeyChecking=no target/ai-leads.war ec2-user@172.31.20.74:/opt/Tomcat10/webapps "
                    sh "ssh ec2-user@172.31.20.74 /opt/Tomcat10/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.20.74 /opt/Tomcat10/bin/startup.sh"
                }

            }
        }
    }
}
