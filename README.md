TASK-01

# Deploying a Static Website on AWS with CloudFront and GitHub Actions

This guide walks through the process of hosting a static website on AWS S3, setting up CloudFront for CDN caching, and automating deployments using GitHub Actions.

## Prerequisites
- AWS Account
- GitHub Repository
- Basic knowledge of HTML/CSS

## Steps Performed

### 1. Create an S3 Bucket for Hosting
- Created an S3 bucket with a unique name.
- Enabled **Static Website Hosting**.
- Configured **Bucket Policy** to allow public access.
- Uploaded website files (HTML, CSS, JS).

### 2. Automate Deployment with GitHub Actions
- Created a `.github/workflows/deploy.yml` file.
- Configured AWS credentials using GitHub Secrets.
- Set up a GitHub Actions workflow to automatically upload files to S3 on every push.

### 3. Set Up CloudFront for CDN Caching
- Created a **CloudFront Distribution** linked to the S3 bucket.
- Configured it to serve files from S3 with caching enabled.
- Generated a **CloudFront URL** to access the website globally.

### 4. CloudFront Invalidation for Automatic Cache Updates
- Added a step in GitHub Actions to **invalidate the CloudFront cache** after each deployment.
- Updated IAM permissions to allow CloudFront invalidation.

### 5. Organized Project Structure
- Moved website files into a dedicated folder.
- Updated GitHub Actions to reference the new folder.
- Ensured `index.html` links were correctly updated.

### 6. Verified Deployment
- Accessed the website via the **CloudFront URL**.
- Tested automated deployments by making small changes and pushing them to GitHub.

## Final Outcome 🎉
✅ A fully automated, globally accessible static website hosted on AWS!

### Access the Website: https://dux1fr7e5n4gg.cloudfront.net


---


TASK-02

# **Flask App Deployment with Docker & GitHub Actions on AWS EC2**

## **Overview**
This project demonstrates how to containerize a Flask application and automate its deployment using **GitHub Actions** on an **AWS EC2** instance. It includes setting up the environment, writing a Dockerfile, configuring a CI/CD pipeline, and handling common deployment challenges.

## **Tech Stack**
- **Python 3.9**
- **Flask**
- **Docker**
- **GitHub Actions**
- **AWS EC2**

## **Setup & Deployment**
### **1. AWS EC2 Configuration**
- Launch an **Ubuntu EC2 instance**.
- Install **Docker**:
  ```bash
  sudo apt update
  sudo apt install docker.io -y
  ```
- Set up **SSH access** for GitHub Actions.

### **2. Flask App Containerization**
- **Dockerfile**:
  ```dockerfile
  FROM python:3.9
  WORKDIR /app
  COPY . .
  RUN pip install -r requirements.txt
  CMD ["python", "app.py"]
  ```
- Build and run locally:
  ```bash
  docker build -t flask-app .
  docker run -d -p 5000:5000 flask-app
  ```

### **3. GitHub Actions Workflow**
- **`.github/workflows/deploy.yml`**:
  ```yaml
  name: Deploy Flask App
  on:
    push:
      branches:
        - main
  jobs:
    deploy:
      runs-on: ubuntu-latest
      steps:
        - name: Checkout Code
          uses: actions/checkout@v3
        
        - name: Deploy to EC2
          run: |
            ssh -o StrictHostKeyChecking=no -i ~/.ssh/id_rsa ubuntu@${{ secrets.EC2_HOST }} << 'EOF'
              cd /home/ubuntu
              git pull origin main
              sudo docker stop myapp || true
              sudo docker rm myapp || true
              sudo docker build -t myapp .
              sudo docker run -d -p 5000:5000 myapp
            EOF
  ```

## **Common Issues & Fixes**
### **1. Port 5000 Already in Use**
```bash
sudo docker stop $(sudo docker ps -q)
```
### **2. SSH Authentication Failure**
- Ensure the private key is correctly added to **GitHub Secrets**.
### **3. Docker Build Caching Issues**
- Use `--no-cache` for a fresh build:
  ```bash
  docker build --no-cache -t flask-app .
  ```

## **Repository**
🔗 [GitHub Repo](https://github.com/kishangupta2079/code2deploy/tree/main/flask_App_Containerized_in_docker_on_EC2)

## **Conclusion**
This setup automates the deployment process, ensuring a **streamlined and efficient CI/CD pipeline** for Flask applications using **Docker and AWS EC2**.
