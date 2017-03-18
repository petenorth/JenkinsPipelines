node('maven') {
  stage 'clone repo'
  git 'https://github.com/petenorth/camel-cxf-wsdl-first-spring-boot.git'
  stage 'build'
  sh 'mvn clean install -settings configuration/settings.xml'
}
