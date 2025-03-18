Day 1 (18/03/2025)

# static-hosting-maverick

# 🚀 AWS S3 Static Website Deployment  

Deploy a static website to **AWS S3** with **GitHub Actions** automation.  

## 📌 Steps Followed  

1️⃣ **Created S3 Bucket**  
- Enabled **Static Website Hosting**  
- Updated **Bucket Policy** for public access  

2️⃣ **Configured GitHub Secrets**  
- `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`, `S3_BUCKET_NAME`  

3️⃣ **Automated Deployment** (GitHub Actions)  
- Pushed `index.html` to S3 using:  
  ```sh
  aws s3 cp index.html s3://static-hosting-maverick/
  ```
- Removed `--acl public-read` to avoid errors  

4️⃣ **Access Website**  
🔗 **URL:** `http://static-hosting-maverick.s3-website.ap-south-1.amazonaws.com` 

---

🎯 **Result:** Website is **live & auto-deploys** on every push! 🚀  
