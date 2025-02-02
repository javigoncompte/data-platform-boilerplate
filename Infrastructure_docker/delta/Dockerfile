FROM apache/spark-py:3.5.0

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    SPARK_HOME=/opt/spark \
    DELTA_VERSION=3.1.0

# Install Python dependencies
RUN pip install --no-cache-dir \
    delta-spark==${DELTA_VERSION} \
    pandas \
    pyarrow

# Download Delta Lake dependencies
RUN cd ${SPARK_HOME}/jars && \
    wget https://repo1.maven.org/maven2/io/delta/delta-core_2.12/${DELTA_VERSION}/delta-core_2.12-${DELTA_VERSION}.jar && \
    wget https://repo1.maven.org/maven2/io/delta/delta-storage/${DELTA_VERSION}/delta-storage-${DELTA_VERSION}.jar

WORKDIR /opt/spark/work-dir

CMD ["python3"] 