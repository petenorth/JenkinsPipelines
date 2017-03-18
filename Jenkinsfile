node('fis2') {
  stage 'clone repo'
  git 'https://github.com/petenorth/camel-cxf-wsdl-first-spring-boot.git'
  stage 'build'
  sh 'ls -l /tmp/.m2/repository'
  sh 'mvn clean install -settings configuration/settings.xml -X'
}
