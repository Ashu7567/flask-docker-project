# Base Image
FROM python:3.9-slim

# Set working directory inside container
WORKDIR /app

# Copy requirement file and install
COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

# Copy app code
COPY . .
RUN pip install pytest

# Expose port
EXPOSE 5000

# Command to run the app
CMD ["python", "app.py"]
