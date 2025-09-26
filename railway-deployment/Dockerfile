# Use Python 3.11 slim image (compatible with all your packages)
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Copy requirements first for better caching
COPY requirements.txt .

# Install build tools, upgrade pip, install dependencies, then remove build tools
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    python3-dev \
    gfortran \
    gcc \
    g++ \
    && python -m pip install --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt \
    && apt-get purge -y --auto-remove build-essential python3-dev gfortran gcc g++ \
    && rm -rf /var/lib/apt/lists/*

# Copy application code
COPY . .

# Set environment variables
ENV PYTHONUNBUFFERED=1

# Expose port (Railway will override with $PORT)
EXPOSE 8000

# Start the FastAPI application with uvicorn (2 workers for concurrency)
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--workers", "2"]