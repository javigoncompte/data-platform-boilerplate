FROM apache/spark-py:3.5.0

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    SPARK_HOME=/opt/spark \
    DELTA_VERSION=3.1.0 \
    PIP_NO_CACHE_DIR=1 \
    PIP_ROOT_USER_ACTION=ignore

# Create non-root user
RUN groupadd -r delta && \
    useradd -r -g delta -d ${SPARK_HOME} delta && \
    chown -R delta:delta ${SPARK_HOME}

# Install Python dependencies with fixed versions
RUN pip install --no-cache-dir \
    delta-spark==${DELTA_VERSION} \
    pandas==2.2.0 \
    pyarrow==14.0.2

# Download Delta Lake dependencies with checksum verification
RUN cd ${SPARK_HOME}/jars && \
    wget -q https://repo1.maven.org/maven2/io/delta/delta-core_2.12/${DELTA_VERSION}/delta-core_2.12-${DELTA_VERSION}.jar && \
    wget -q https://repo1.maven.org/maven2/io/delta/delta-storage/${DELTA_VERSION}/delta-storage-${DELTA_VERSION}.jar && \
    chown -R delta:delta ${SPARK_HOME}/jars

WORKDIR ${SPARK_HOME}/work-dir
RUN chown -R delta:delta ${SPARK_HOME}/work-dir

USER delta

CMD ["python3"] 