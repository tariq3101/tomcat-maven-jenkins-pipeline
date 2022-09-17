create jenkins server on centos 7
give root credentials to jenkins user.
 
 vi /lib/systemd/system/jenkins.service 
or
/usr/lib/systemd/system/jenkins.service;

: change from jenkins to root in user and group

# $JENKINS_HOME, $JENKINS_LOG, and (if you have already run Jenkins)
# $JENKINS_WEBROOT.
User=root
Group=root    

systemctl daemon-reload

systemctl status jenkins

systemctl restart jenkins

 After jenkins server is created , create a tomcat server ...
 
 steps are there in tomcat-server repo...
-----------------

Start jenkins and configure it ..

yum install maven -y

yum install git -y

mvn --version

https://github.com/ramannkhanna2/hello-world-maven-pipeline.git

under execute shell >>

mvn clean
mvn package


--- from dashboard , add "deploy to container" plugin 
under post build steps >> add deploy to container , mention tomcat server's username and password and url to deploy

WAR/EAR files >> **/*.war

SAVE AND BUILD
