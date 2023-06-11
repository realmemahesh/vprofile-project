FROM openjdk:11 AS BUILD-IMAGE
RUN apt update && apt install maven -y 
RUN git clone https://github.com/realmemahesh/vprofile-project.git 
RUN cd vprofile-project && git checkout docker && mvn install

FROM tomcat:9-jre11
LABEL "Project"="vprofile"
LABEL "Author"="Mahesh"
ENV CATALINA_HOME=/usr/local/tomcat
RUN rm -rf $CATALINA_HOME/webapps/*
COPY --from=BUILD-IMAGE vprofile-project/target/vprofile-v2.war /$CATALINA_HOME/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh","run"]