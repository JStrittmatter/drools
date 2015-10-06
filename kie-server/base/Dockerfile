#################################################################################
# Dockerfile image that provides JBoss KIE Server 6.2.0.Final
#
# The web application binaries are downloaded from JBoss Nexus Repository.
#
# The Docker image generated name/tag is "jboss/kie-server:6.2.0.Final"
#################################################################################

####### BASE ############
FROM jboss/wildfly:8.2.1.Final

####### MAINTAINER ############
MAINTAINER "Roger Martinez" "romartin@redhat.com"

####### ENVIRONMENT ############
ENV KIE_REPOSITORY https://repository.jboss.org/nexus/content/groups/public-jboss/
ENV DROOLS_VERSION 6.3.0-SNAPSHOT
ENV DROOLS_SNAPSHOT_VERSION 6.3.0-20150529.093400-608
ENV DROOLS_CLASSIFIER ee7
ENV DROOLS_CONTEXT_PATH kie-server
ENV JAVA_OPTS -XX:MaxPermSize=256m -Xms256m -Xmx512m

####### CUSTOM JBOSS USER ############
# Switchback to jboss user
USER jboss

####### KIE-SERVER ############
RUN curl -o /opt/jboss/$DROOLS_CONTEXT_PATH.war $KIE_REPOSITORY/org/kie/kie-server/$DROOLS_VERSION/kie-server-$DROOLS_SNAPSHOT_VERSION-$DROOLS_CLASSIFIER.war && \ 
unzip -q /opt/jboss/$DROOLS_CONTEXT_PATH.war -d /opt/jboss/wildfly/standalone/deployments/$DROOLS_CONTEXT_PATH.war &&  \ 
touch /opt/jboss/wildfly/standalone/deployments/$DROOLS_CONTEXT_PATH.war.dodeploy &&  \ 
rm -rf /opt/jboss/$DROOLS_CONTEXT_PATH.war

####### RUNNING KIE-SERVER ############
WORKDIR /opt/jboss/wildfly/bin/
CMD ["./standalone.sh", "-b", "0.0.0.0", "--server-config=standalone-full.xml", "-Dorg.kie.server.id=${KIE_SERVER_ID}", "-Dorg.kie.server.location=${KIE_SERVER_LOC}", "-Dorg.kie.server.controller=${CONTROLLER_LOC}", "-Dorg.kie.server.controller.user=${CONTROLLER_USER}", "-Dorg.kie.server.controller.pwd=${CONTROLLER_PWD}"]
