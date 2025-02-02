FROM apache/spark-py:3.5.0

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    SPARK_HOME=/opt/spark \
    ICEBERG_VERSION=1.5.0 \
    AWS_SDK_VERSION=2.20.18

# Install Python dependencies
RUN pip install --no-cache-dir \
    pyiceberg==${ICEBERG_VERSION} \
    pandas \
    boto3

# Download Iceberg Spark Runtime
RUN cd ${SPARK_HOME}/jars && \
    wget https://repo1.maven.org/maven2/org/apache/iceberg/iceberg-spark-runtime-3.5_2.12/${ICEBERG_VERSION}/iceberg-spark-runtime-3.5_2.12-${ICEBERG_VERSION}.jar && \
    wget https://repo1.maven.org/maven2/software/amazon/awssdk/bundle/${AWS_SDK_VERSION}/bundle-${AWS_SDK_VERSION}.jar && \
    wget https://repo1.maven.org/maven2/software/amazon/awssdk/url-connection-client/${AWS_SDK_VERSION}/url-connection-client-${AWS_SDK_VERSION}.jar

WORKDIR /opt/spark/work-dir

CMD ["python3"] 