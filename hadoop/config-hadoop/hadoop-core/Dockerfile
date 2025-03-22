# Base Image
FROM ubuntu:22.04

# Set root password
RUN echo "root:root" | chpasswd

# Update and install required packages
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y openjdk-8-jdk wget ssh openssh-server dos2unix vim sudo telnet iputils-ping && \
    apt-get clean

# Set environment variables
ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
ENV HADOOP_HOME=/home/hadooptanhung/hadoop
ENV PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$JAVA_HOME/bin

# Create user hadooptanhung
RUN adduser --disabled-password --gecos "" hadooptanhung && \
    echo "hadooptanhung:hadooptanhung" | chpasswd && \
    usermod -aG sudo hadooptanhung && \
    echo "hadooptanhung ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Install Hadoop
USER hadooptanhung

WORKDIR /home/hadooptanhung
RUN wget https://dlcdn.apache.org/hadoop/common/hadoop-3.4.1/hadoop-3.4.1.tar.gz && \
    tar -xzf hadoop-3.4.1.tar.gz && \
    mv hadoop-3.4.1 hadoop && \
    rm hadoop-3.4.1.tar.gz

# Set JAVA_HOME in hadoop-env.sh
RUN echo "export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64" >> /home/hadooptanhung/hadoop/etc/hadoop/hadoop-env.sh
    

# Copy Hadoop configuration files
COPY .bashrc /home/hadooptanhung/.bashrc

RUN mkdir -p /home/hadooptanhung/.ssh && \
    ssh-keygen -t rsa -P '' -f /home/hadooptanhung/.ssh/id_rsa && \
    cat /home/hadooptanhung/.ssh/id_rsa.pub >> /home/hadooptanhung/.ssh/authorized_keys && \
    chmod 600 /home/hadooptanhung/.ssh/authorized_keys && \
    chown -R hadooptanhung:hadooptanhung /home/hadooptanhung/.ssh

# Add permission to ssh folder and keys
USER root

# Convert files to Unix format
RUN dos2unix /home/hadooptanhung/.bashrc 

# Expose ports
EXPOSE 9000 50070 9001 9002 9003 9004 9005 9006 9870 9864 8088 8042
