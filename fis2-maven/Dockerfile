FROM registry.access.redhat.com/openshift3/jenkins-slave-maven-rhel7

USER root

RUN cd ~ && pwd

RUN cd $HOME && git clone https://github.com/petenorth/camel-cxf-wsdl-first-spring-boot.git && cd camel-cxf-wsdl-first-spring-boot && mvn clean -s configuration/settings.xml

RUN ls ~/.m2

USER 1001

