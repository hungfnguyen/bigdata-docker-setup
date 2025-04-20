FROM hadoop-master

USER hadooptanhung
WORKDIR /home/hadooptanhung/


RUN wget https://dlcdn.apache.org/hive/hive-4.0.1/apache-hive-4.0.1-bin.tar.gz && \
    tar -xvzf apache-hive-4.0.1-bin.tar.gz && \
    mv apache-hive-4.0.1-bin hive && \
    rm apache-hive-4.0.1-bin.tar.gz

COPY conf/.bashrc /home/hadooptanhung/.bashrc 
COPY conf/hive-site.xml /home/hadooptanhung/hive/conf/ 
COPY conf/hive-env.sh /home/hadooptanhung/hive/conf/


USER root
RUN dos2unix /home/hadooptanhung/.bashrc && \
    dos2unix /home/hadooptanhung/hive/conf/hive-site.xml && \
    dos2unix /home/hadooptanhung/hive/conf/hive-env.sh && \
    apt-get update && \
    apt-get install -y net-tools


# CMD ["/bin/bash", "-c", "service ssh start && bash"]
#CMD ["/bin/bash", "-c", "service ssh start && /home/hadooptanhung/hive/bin/hive --service hiveserver2 > /home/hadooptanhung/hiveserver2.log 2>&1"]
# hdfs dfs -mkdir -p /user/hive/warehouse && \
# hdfs dfs -chmod g+w /user/hive/warehouse && \

CMD ["/bin/bash", "-c", "\
    service ssh start && \
    /home/hadooptanhung/hive/bin/hive --service hiveserver2 > /home/hadooptanhung/hiveserver2.log 2>&1"]



