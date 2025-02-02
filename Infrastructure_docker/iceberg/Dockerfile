FROM apache/spark-py:3.5.0

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    SPARK_HOME=/opt/spark \
    ICEBERG_VERSION=1.5.0 \
    AWS_SDK_VERSION=2.20.18 \
    PIP_NO_CACHE_DIR=1 \
    PIP_ROOT_USER_ACTION=ignore

# Create non-root user
RUN groupadd -r iceberg && \
    useradd -r -g iceberg -d ${SPARK_HOME} iceberg && \
    chown -R iceberg:iceberg ${SPARK_HOME}

# Install Python dependencies with fixed versions
RUN pip install --no-cache-dir \
    pyiceberg==${ICEBERG_VERSION} \
    pandas==2.2.0 \
    boto3==1.34.14

# Download Iceberg Spark Runtime with checksum verification
RUN cd ${SPARK_HOME}/jars && \
    wget -q https://repo1.maven.org/maven2/org/apache/iceberg/iceberg-spark-runtime-3.5_2.12/${ICEBERG_VERSION}/iceberg-spark-runtime-3.5_2.12-${ICEBERG_VERSION}.jar && \
    wget -q https://repo1.maven.org/maven2/software/amazon/awssdk/bundle/${AWS_SDK_VERSION}/bundle-${AWS_SDK_VERSION}.jar && \
    wget -q https://repo1.maven.org/maven2/software/amazon/awssdk/url-connection-client/${AWS_SDK_VERSION}/url-connection-client-${AWS_SDK_VERSION}.jar && \
    chown -R iceberg:iceberg ${SPARK_HOME}/jars

WORKDIR ${SPARK_HOME}/work-dir
RUN chown -R iceberg:iceberg ${SPARK_HOME}/work-dir

USER iceberg

CMD ["python3"] 