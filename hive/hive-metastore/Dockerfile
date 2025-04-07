FROM openjdk:8-jdk

# Thiết lập các biến môi trường cần thiết
ENV JAVA_HOME=/usr/local/openjdk-8
ENV PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:${PATH}"

# Cài đặt các công cụ cần thiết
RUN apt-get update && apt-get install -y \
    netcat-traditional \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Thiết lập thư mục làm việc
WORKDIR /opt

# Thiết lập các biến môi trường cho Hive Metastore
ENV METASTORE_VERSION=3.0.0
ENV HIVE_HOME=/opt/apache-hive-metastore-${METASTORE_VERSION}-bin

# Tải và giải nén Hive Metastore standalone
RUN curl -L https://archive.apache.org/dist/hive/hive-standalone-metastore-${METASTORE_VERSION}/hive-standalone-metastore-${METASTORE_VERSION}-bin.tar.gz | tar zxf -

# Tải MySQL Connector và copy vào thư mục lib của Hive
RUN curl -L https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-8.0.19.tar.gz | tar zxf - && \
    cp mysql-connector-java-8.0.19/mysql-connector-java-8.0.19.jar ${HIVE_HOME}/lib/ && \
    rm -rf mysql-connector-java-8.0.19

# Copy file cấu hình metastore-site.xml
COPY metastore-site.xml ${HIVE_HOME}/conf/

# Copy entrypoint script để khởi động Hive Metastore
COPY entrypoint.sh /entrypoint.sh

# Tạo user 'hive' để chạy container không dùng quyền root
RUN groupadd -r hive --gid=1000 && \
    useradd -r -g hive --uid=1000 -d ${HIVE_HOME} hive && \
    chown -R hive:hive ${HIVE_HOME} && \
    chown hive:hive /entrypoint.sh && chmod +x /entrypoint.sh

# Chỉ expose cổng Metastore (9083)
USER hive
EXPOSE 9083

# ENTRYPOINT: chạy script entrypoint.sh khi container khởi động
ENTRYPOINT ["/entrypoint.sh"]
