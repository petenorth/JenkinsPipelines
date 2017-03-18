FROM registry.access.redhat.com/openshift3/jenkins-slave-maven-rhel7

USER root

RUN cd /tmp && git clone https://github.com/petenorth/camel-cxf-wsdl-first-spring-boot.git && cd camel-cxf-wsdl-first-spring-boot && mvn clean install -s configuration/settings.xml && cp -f configuration/settings.xml /tmp/.m2

RUN cp -r /root/.m2/repository /tmp/.m2 

RUN chown -R 1001:0 /tmp/.m2 && \
    chmod -R g+rw /tmp/.m2

USER 1001

