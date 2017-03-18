FROM registry.access.redhat.com/openshift3/jenkins-slave-maven-rhel7

USER root

RUN cd $HOME && git clone https://github.com/petenorth/camel-cxf-wsdl-first-spring-boot.git && cd camel-cxf-first-spring-boot && mvn clean install -s configuration/settings.xml

