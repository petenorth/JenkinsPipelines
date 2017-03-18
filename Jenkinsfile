node('maven') {
  stage 'clone repo'
  git 'https://github.com/petenorth/spring-boot-cxf-jaxrs.git'
  stage 'build'
  sh 'mvn clean install'
}
