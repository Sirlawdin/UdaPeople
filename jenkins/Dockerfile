#Jenkins base image.

FROM node:16 AS builder

ENV WORKING_DIR=/usr/app/src/

WORKDIR ${WORKING_DIR}

RUN echo 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' >> /etc/apt/sources.list \
&& apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 \
&& apt update \
&& apt install -y ansible sshpass

RUN apt install -y python-pip && \
pip install docker

ADD https://nibss-dev.github.io/Jenkins-Packages/pm2.tar.gz .


RUN apt-get install -y apt-transport-https ca-certificates curl unzip software-properties-common && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/debian \
       $(lsb_release -cs) \
       stable" && \
    apt update && \
    apt install -y docker-ce docker-ce-cli containerd.io

# Install Java (JRE and JDK) and Maven
RUN apt-get update && apt-get install -y \
    default-jre \
    default-jdk \
    maven

# Define the MAVEN_HOME environment variable
ENV MAVEN_HOME /usr/share/maven

# Add MAVEN_HOME to PATH
ENV PATH $MAVEN_HOME/bin:$PATH