currentBuild.displayName = "online-shopping-#"+currentBuild.number

pipeline{
    agent any
/*    
     environment{
        PATH = "/opt/maven3/bin:$PATH"
     }
 */   
    tools {
        maven 'm1'
    }

    
    stages{
        stage("Git Checkout"){
            steps{
                git credentialsId: 'github', url: 'https://github.com/ramannkhanna2/tomcat-maven-jenkins-pipeline.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
                sh "mv webapp/target/*.war webapp/target/myweb.war"
            }
        }
        stage("deploy-dev"){
            steps{
                sshagent(['tomcat-new']) {
                sh """
                    scp -o StrictHostKeyChecking=no webapp/target/myweb.war  centos@44.204.8.191:/opt/apache-tomcat-9.0.78/webapps

                    ssh centos@44.204.8.191 /opt/apache-tomcat-9.0.78/bin/shutdown.sh
                    
                    ssh centos@44.204.8.191 /opt/apache-tomcat-9.0.78/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}
