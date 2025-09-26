# Use Python 3.9 slim image
FROM python:3.9-slim

# Update system and install build-essential, plus necessary development tools for pandas
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    python3-dev \
    gfortran \
    && rm -rf /var/lib/apt/lists/*

# Ensure pip is available and upgraded
RUN python -m ensurepip --upgrade
RUN python -m pip install --upgrade pip
RUN which pip && pip --version

# Set working directory
WORKDIR /app

# Copy requirements first for better caching
COPY requirements.txt .

# Debug: Check if pip is available and show Python/pip versions
RUN python --version && pip --version

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Set environment variables
ENV PORT=8000
ENV PYTHONUNBUFFERED=1

# Expose port
EXPOSE 8000

# Start the FastAPI application
CMD ["python", "main.py"]