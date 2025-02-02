FROM rayproject/ray:2.9.0-py39

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    RAY_HOME=/opt/ray

# Install additional Python packages
RUN pip install --no-cache-dir \
    'ray[data]' \
    'ray[train]' \
    pandas \
    pyarrow \
    numpy \
    scikit-learn

# Create working directory
WORKDIR /opt/ray/work-dir

# Expose Ray dashboard and other ports
EXPOSE 8265 10001 6379

# Default command to start Ray head node
CMD ["ray", "start", "--head", "--dashboard-host=0.0.0.0"] 