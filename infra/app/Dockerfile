FROM jenkins/jenkins:lts
USER root

COPY init.groovy.d/basic-security.groovy /usr/share/jenkins/ref/init.groovy.d/basic-security.groovy
COPY init.groovy.d/basic-security.groovy /usr/share/jenkins/ref/init.groovy.d/disable-crumb.groovy

EXPOSE 8080

ENV JENKINS_OPTS="--httpPort=80"

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt
