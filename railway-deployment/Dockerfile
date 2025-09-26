# Use Python 3.9 slim image
FROM python:3.9-slim

# Update system and ensure pip is available
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Ensure pip is available and upgraded
RUN python -m ensurepip --upgrade
RUN python -m pip install --upgrade pip
RUN which pip && pip --version

# Set working directory
WORKDIR /app
