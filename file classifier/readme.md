
# 📂 Automatically Classifier for Folders

This project automatically classifies incoming **text files** uploaded to an **Amazon S3 bucket** into predefined categories like **Finance**, **Healthcare**, and **Education**.  
It uses **AWS Lambda** + **Amazon Comprehend** for Natural Language Processing (NLP) to detect the topic of each file and then **moves the file** to the appropriate folder inside the bucket.

---

## 🚀 Project Architecture

1. **Amazon S3**  
   - Stores uploaded `.txt` files.
   - Triggers the Lambda function when a new file is uploaded.

2. **AWS Lambda**  
   - Executes Python code to:
     - Read the uploaded text file.
     - Call **Amazon Comprehend** for classification.
     - Move the file into a categorized folder inside the S3 bucket.

3. **Amazon Comprehend**  
   - Performs **text classification** using AWS's pre-trained NLP models.

4. **IAM Roles & Permissions**  
   - Lambda is assigned an IAM Role with policies:
     - `AmazonS3FullAccess`
     - `ComprehendFullAccess`
     - `CloudWatchLogsFullAccess`

---

## 🛠️ Setup Instructions

### **1. Create an S3 Bucket**
- Go to **S3 Console** → Create a bucket.
- Name it something like:
