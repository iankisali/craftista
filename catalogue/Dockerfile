# ----------------------------------------------
# Stage 1: Build the Python Flask microservice application
# ----------------------------------------------

# Using Python base image based on alpine
FROM python:3.12.10-alpine3.21

# Set the working directory inside the container
WORKDIR /app

# Copy the project's requirements file to the container
COPY requirements.txt .

# Installing the application dependencies using pip from a requirements file
RUN pip install -r requirements.txt

# Copy the application into the container
COPY . .

# Expose port 5000 for the Python Flask application
EXPOSE 5000

# Define the command to run the Python Flask application
CMD ["gunicorn", "app:app", "--bind", "0.0.0.0:5000"]
