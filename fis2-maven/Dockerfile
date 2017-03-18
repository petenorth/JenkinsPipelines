FROM registry.access.redhat.com/openshift3/jenkins-slave-maven-rhel7

USER root

RUN cd $HOME && git clone https://github.com/petenorth/camel-cxf-wsdl-first-spring-boot.git && cd camel-cxf-wsdl-first-spring-boot && mvn clean install -s configuration/settings.xml

RUN cp -r /root/.m2/repository $HOME/.m2 && cp -f configuration/settings.xml $HOME/.m2

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001

