FROM python:3.10-slim

# Install necessary system packages
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    libopenblas-dev \
    liblapack-dev \
    libx11-dev \
    libgtk-3-dev \
    libboost-all-dev \
    libssl-dev \
    libffi-dev \
    python3-dev \
    curl \
    tzdata && \
    ln -fs /usr/share/zoneinfo/Asia/Kolkata /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Install Python dependencies
COPY requirements.txt .
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Environment variables
ENV TZ=Asia/Kolkata
ENV FLASK_APP=app.py
ENV FLASK_ENV=production

# Expose the new port
EXPOSE 8000

# Run the app with Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "app:app"]
