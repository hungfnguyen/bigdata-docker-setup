FROM jupyter/all-spark-notebook:python-3.9.13

USER root

RUN curl -O https://archive.apache.org/dist/spark/spark-3.3.2/spark-3.3.2-bin-hadoop3.tgz \
    && tar zxvf spark-3.3.2-bin-hadoop3.tgz \
    && rm -rf spark-3.3.2-bin-hadoop3.tgz \
    && mv spark-3.3.2-bin-hadoop3/ /usr/local/ \
    && rm -rf /usr/local/spark \
    && ln -s /usr/local/spark-3.3.2-bin-hadoop3 /usr/local/spark
