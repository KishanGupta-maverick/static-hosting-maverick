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

### Access the Website: [Your CloudFront URL]
(Replace with actual CloudFront URL)

---