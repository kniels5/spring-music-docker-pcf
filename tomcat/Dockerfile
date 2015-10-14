# Apache Tomcat image with build artifact

FROM tomcat:DFS8.0

MAINTAINER Keith Nielsen <keithnielsen@discover.com>

#Expose exposes ports on the container to the local host, should not include port mapping in dockerfile
# instead should allow creator the container to specify it with -p option


#Pull in the latest build from Nexus
ENV NEXUS_REPO http://172.16.118.132:8081/nexus/content/repositories/releases

# This will be injected by Jenkins build job as it builds and deploys the app container
ENV APP_FILE_NAME spring-music-13.war

# Install wget and use it to install the application in the file system
RUN apt-get update -y && \
  apt-get install wget -y && \
  wget -O --http-user=admin --http-passwd=admin /usr/local/tomcat/webapps/ROOT.war ${NEXUS_REPO}/${APP_FILE_NAME} && \
  mv /usr/local/tomcat/webapps/ROOT /usr/local/tomcat/webapps/_ROOT

COPY tomcat-users.xml /usr/local/tomcat/conf/tomcat-users.xml
