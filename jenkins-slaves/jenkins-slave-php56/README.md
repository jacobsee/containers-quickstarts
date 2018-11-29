# jenkins-slave-php56
Provides a docker image of the PHP 5.6 runtime for use as a Jenkins slave.

## Build local
`docker build -t jenkins-slave-php56 .`

## Run local
For local running and experimentation run `docker run -i -t jenkins-slave-php56 /bin/bash` and have a play once inside the container.

## Build in OpenShift
```bash
oc process -f ../templates/jenkins-slave-generic-template.yml \
    -p NAME=jenkins-slave-php56 \
    -p SOURCE_CONTEXT_DIR=jenkins-slaves/jenkins-slave-php56 \
    -p DOCKERFILE_PATH=Dockerfile \
    | oc create -f -
```
For all params see the list in the `../templates/jenkins-slave-generic-template.yml` or run `oc process --parameters -f ../templates/jenkins-slave-generic-template.yml`.

## Jenkins
Add a new Kubernetes Container template called `jenkins-slave-php56` (if you've build and pushed the container image locally) and specify this as the node when running builds. If you're using the template attached; the `role: jenkins-slave` is attached and Jenkins should automatically discover the slave for you. Further instructions can be found [here](https://docs.openshift.com/container-platform/3.7/using_images/other_images/jenkins.html#using-the-jenkins-kubernetes-plug-in-to-run-jobs). PHP installation commands are very slightly modified from the SCL versions, which can be found [here](https://github.com/sclorg/s2i-php-container/tree/master/5.6).