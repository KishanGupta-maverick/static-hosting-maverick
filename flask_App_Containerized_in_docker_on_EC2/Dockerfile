FROM python:3.9  

# Set the working directory
WORKDIR /app  

# Copy the requirements file separately to leverage Docker's caching mechanism
COPY requirements.txt .  

# Install dependencies and clear pip cache
RUN pip install --no-cache-dir -r requirements.txt  

# Copy the rest of the application files
COPY . .  

# Set the command to run the application
CMD ["python", "app.py"]
