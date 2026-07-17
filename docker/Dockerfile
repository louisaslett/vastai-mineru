#For example
FROM vastai/base-image:cuda-13.2.0-auto

# Install your applications into /opt/workspace-internal/
# This ensures files can be properly synced between instances
WORKDIR /opt/workspace-internal/

# Activate virtual environment from base image
RUN . /venv/main/bin/activate

# 1. Install mineru
RUN <<EOF
  uv venv
  source .venv/bin/activate
  uv pip install -U "mineru[core]"
EOF

# 2. Pre-download all models during the image build phase
RUN <<EOF
  source .venv/bin/activate
  TORCH_DEVICE_BACKEND_AUTOLOAD=0 mineru-models-download -s huggingface -m all
EOF

# 3. Force MinerU to use the local models at runtime
ENV MINERU_MODEL_SOURCE=local
