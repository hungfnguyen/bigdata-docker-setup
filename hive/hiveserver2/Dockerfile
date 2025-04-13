FROM hadoop-pig

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
    dos2unix /home/hadooptanhung/hive/conf/hive-env.sh


CMD ["/bin/bash", "-c", "service ssh start && bash"]



