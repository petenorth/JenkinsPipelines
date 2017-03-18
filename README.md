#JenkinsPipelines

##Introduction

This project demonstrates how to speed up maven builds when using PipelineStrategy within Openshift.

Openshift will create a Jenkins pod automatically when a build configuration is created which uses the PipelineStrategy.

When the pipeline is started within Openshift Jenkins will read the contents of the Jenkinsfile contained within the build configuration and when it encounters function calls node(...) will try and match the string argument to a pod template configured within the main Jenkins instance. The pod template lists containers and associated docker images that will be used when creating a slave pod which will carry out the tasks listed in the node(...) function body.

Openshift ships with 2 default pod templates, one for nodejs and one for maven. These templates are meant to be general purpose slave images.Focusing on Maven, the general purpose nature means that it has an empty local maven repository cache. So every time a build using the slave is executed it must download everything.

For s2i builds there are features such as incremental builds and/or placing a nexus instance as a pod in Openshift to minimise network traffic etc. . The latter is of some use for Openshift Jenkins slave image builds but it isn't that great. Builds will still take too long.

An alternative approach is to look at what is downloaded during a build? In the case of a FIS 2.0 well structured project it will be

  1) A standard set of plugins.
  2) The dependencies managed by the FIS 2.0 Fabric8 maven BOM.
  
This is similar to the system repository of the Fuse install or a offline repo. It won't change very frequently and represents 90% of the artifacts downloaded. So based on this lets create a derived docker image based on the maven slave image shipped with the Openshift product and then configure Jenkins to recognize this image.

##Installation/Build

Create a build config to build the derived image

    oc new-build https://github.com/petenorth/JenkinsPipelines.git --context-dir=fis2-maven
    
Once build look at the image stream created and get the registry location something like

    172.30.5.30:5000/sample-project/jenkinspipelines
    
Go to the Jenkins instance and after logging in as admin click on 'manage jenkins'. Navigate to the kubernetes jenkins plugin section and create a new pod template based on the one called maven. Give a name and label of fis2 and specify the docker image as the registry location previously noted. Make sure the Jenkins Slave root directory is /tmp .

All that remains is to create a build config from the yaml

    oc create -f buildconfig.yaml

If you examines the logs you should see that very little is downloaded and the build zips along, be aware that the first build may be slow as it needs to retrieve the fis2 image that has been built.
