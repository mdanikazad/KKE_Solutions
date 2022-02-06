pipeline {
    agent any
    environment {
        PATH = "/opt/apache-maven-3.6.3/bin:$PATH"
    }
    stages {
        stage("clone code"){
            steps{
               git credentialsId: '37101439-1799-4333-bb94-dad4155dfbb8', url: 'https://anishazad@bitbucket.org/anishazad/sample_jhipsterapp_sc.git', branch: 'develop'
            }
        }
        stage("build code"){
            steps{
              sh "./mvnw -Pprod clean package -DskipTests"
            }
        }
        stage("deploy"){
            steps{
              sshagent(['deploy_user']) {
                 sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/dev-bridge_pipe/target/*.war ec2-user@54.158.250.212:/opt/tomcat/webapps/ROOT.war"
                 
                }
            }
        }
    }
}
