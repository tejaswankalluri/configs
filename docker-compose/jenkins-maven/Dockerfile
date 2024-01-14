FROM jenkins/jenkins:lts
# if we want to install via apt
USER root
RUN apt-get update && apt-get install -y maven && apt-get install -y openjdk-17-jdk wget sudo
ENV JAVA_HOME /usr/lib/jvm/java-17-openjdk-amd64

# add docker inside container
RUN wget http://get.docker.com/builds/Linux/x86_64/docker-latest.tgz
RUN tar -xvzf docker-latest.tgz
RUN mv docker/* /usr/bin/

# drop back to the regular jenkins user - good practice
USER jenkins