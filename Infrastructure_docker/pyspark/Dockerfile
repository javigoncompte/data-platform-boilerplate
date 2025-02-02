FROM apache/spark-py:3.5.0

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    SPARK_HOME=/opt/spark \
    PYSPARK_PYTHON=python3 \
    PYSPARK_DRIVER_PYTHON=python3 \
    PIP_NO_CACHE_DIR=1 \
    PIP_ROOT_USER_ACTION=ignore

# Create non-root user
RUN groupadd -r spark && \
    useradd -r -g spark -d ${SPARK_HOME} spark && \
    chown -R spark:spark ${SPARK_HOME}

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3-pip \
    python3-dev \
    && rm -rf /var/lib/apt/lists/* \
    && pip install --no-cache-dir --upgrade pip

# Install Python packages
RUN pip install --no-cache-dir \
    pyspark==3.5.0 \
    pandas==2.2.0 \
    numpy==1.26.3 \
    scikit-learn==1.4.0 \
    matplotlib==3.8.2 \
    seaborn==0.13.1 \
    pyarrow==14.0.2 \
    jupyterlab==4.0.11 \
    plotly==5.18.0 \
    ipywidgets==8.1.1

# Create working directory and set permissions
WORKDIR ${SPARK_HOME}/work-dir
RUN chown -R spark:spark ${SPARK_HOME}/work-dir

# Copy spark-defaults.conf for custom Spark configuration
COPY --chown=spark:spark spark-defaults.conf ${SPARK_HOME}/conf/

# Switch to non-root user
USER spark

# Expose ports for Spark UI and Jupyter
EXPOSE 4040 8888

# Set secure Jupyter configuration
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--NotebookApp.token='sparktoken'"] 