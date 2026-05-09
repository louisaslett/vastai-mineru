#For example
FROM docker pull vastai/base-image:cuda-13.2.0-auto

# Install your applications into /opt/workspace-internal/
# This ensures files can be properly synced between instances
WORKDIR /opt/workspace-internal/

# Activate virtual environment from base image
RUN . /venv/main/bin/activate

RUN uv pip install -U "mineru[core]"
