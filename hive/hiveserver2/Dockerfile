FROM apache/hive:4.0.1

USER root

RUN apt update && apt install -y \
    telnet \
    iputils-ping \
    net-tools \
 && apt clean

USER hive
