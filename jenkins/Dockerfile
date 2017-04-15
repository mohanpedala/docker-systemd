FROM centos/systemd

RUN /usr/bin/yum update -y
RUN /usr/bin/yum -y install \
  git \
  java-1.8.0-openjdk.x86_64 \
RUN groupadd tomcat
#RUN useradd -s /bin/nologin -g tomcat -d /opt/tomcat tomcat
#RUN yum install wget -y
RUN curl -O http://www-us.apache.org/dist/tomcat/tomcat-8/v8.5.13/bin/apache-tomcat-8.5.13.tar.gz
RUN mkdir /opt/tomcat
RUN tar -zxvf apache-tomcat-8.5.13.tar.gz -C /opt/tomcat --strip-components=1
ADD tomcat.service /etc/systemd/system/tomcat.service
RUN chmod -R 777 /opt/tomcat
RUN systemctl start tomcat.service
RUN systemctl enable tomcat.service
EXPOSE 8080
RUN cp /etc/profile /etc/profile_backup
RUN echo 'export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk' | sudo tee -a /etc/profile
RUN echo 'export JRE_HOME=/usr/lib/jvm/jre' | sudo tee -a /etc/profile
RUN source /etc/profile
RUN cd $HOME
RUN curl -O https://updates.jenkins-ci.org/download/war/2.45/jenkins.war
RUN cd /opt/tomcat/webapps
RUN rm -rf *
RUN cp $HOME/jenkins.war /opt/tomcat/webapps/ROOT.war

CMD ["/usr/sbin/init"]
