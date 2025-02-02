FROM rayproject/ray:2.9.0-py39

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    RAY_HOME=/opt/ray \
    PIP_NO_CACHE_DIR=1 \
    PIP_ROOT_USER_ACTION=ignore

# Create non-root user
RUN groupadd -r ray && \
    useradd -r -g ray -d ${RAY_HOME} ray && \
    chown -R ray:ray ${RAY_HOME}

# Install additional Python packages with fixed versions
RUN pip install --no-cache-dir \
    'ray[data]==2.9.0' \
    'ray[train]==2.9.0' \
    pandas==2.2.0 \
    pyarrow==14.0.2 \
    numpy==1.26.3 \
    scikit-learn==1.4.0

# Create working directory and set permissions
WORKDIR ${RAY_HOME}/work-dir
RUN chown -R ray:ray ${RAY_HOME}/work-dir

USER ray

# Expose Ray dashboard and other ports
EXPOSE 8265 10001 6379

# Default command to start Ray head node
CMD ["ray", "start", "--head", "--dashboard-host=0.0.0.0"] 