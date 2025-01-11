# codetech-task1
CREATING  AND CONFIGURING  CLOUD STORAGE ON AWS S3.
# README: Setting Up an S3 Bucket with Versioning and Public Access

## Overview
This guide explains how to create an Amazon S3 bucket, enable versioning, and configure it for public access while minimizing security risks. It is intended for developers or administrators who want to manage an S3 bucket with public accessibility and versioning capabilities.

---

## Prerequisites
1. An AWS account.
2. Basic knowledge of AWS Management Console or AWS CLI.
3. AWS CLI installed and configured (optional for CLI users).

---

## Step 1: Create an S3 Bucket

### Using AWS Management Console:
1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to the *S3* service.
3. Click *Create bucket*.
4. Provide a *Bucket name* (globally unique).
5. Choose an *AWS region*.
6. Keep the default settings or modify as needed.
7. Click *Create bucket*.

### Using AWS CLI:
bash
aws s3api create-bucket --bucket <bucket-name> --region <region> --create-bucket-configuration LocationConstraint=<region>

Replace <bucket-name> and <region> with your desired values.

---

## Step 2: Enable Versioning

### Using AWS Management Console:
1. Open your bucket from the *S3 Dashboard*.
2. Navigate to the *Properties* tab.
3. Find the *Bucket Versioning* section and click *Edit*.
4. Select *Enable* and click *Save changes*.

### Using AWS CLI:
bash
aws s3api put-bucket-versioning --bucket <bucket-name> --versioning-configuration Status=Enabled


---

## Step 3: Configure Public Access

### 3.1: Update Bucket Policy for Public Read Access

Use the following bucket policy to allow public read access to objects:
json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<bucket-name>/*"
        }
    ]
}

Replace <bucket-name> with your bucket name.

#### Steps to Apply the Policy:
1. Open the bucket in the *S3 Dashboard*.
2. Go to the *Permissions* tab.
3. Scroll to the *Bucket Policy* section and paste the above policy.
4. Save the changes.

### 3.2: Disable Block Public Access Settings
1. In the *Permissions* tab, locate the *Block Public Access (Bucket settings)* section.
2. Click *Edit*.
3. Uncheck the "Block all public access" option or adjust settings to allow public access.
4. Confirm changes by typing confirm.

---

## Step 4: Access Public Objects

After configuring public access, objects in the bucket can be accessed via public URLs. For example:

plaintext
https://<bucket-name>.s3.amazonaws.com/<object-key>

Replace <bucket-name> with your bucket name and <object-key> with the file name or path.

---

## Step 5: Mitigating Security Risks

1. *Avoid Sensitive Data*:
   - Do not store sensitive or private data in publicly accessible buckets.

2. *Monitor Bucket Usage*:
   - Enable *AWS CloudTrail* to monitor bucket access.
   - Use *Amazon S3 Access Logs* for tracking.

3. *Use Lifecycle Policies*:
   - Implement lifecycle policies to automatically transition or delete old object versions to save storage costs.

4. *Restrict Actions*:
   - Grant only s3:GetObject permissions for public access to prevent unwanted modifications.

5. *Set Expiration for Public URLs*:
   - Use *Pre-signed URLs* for temporary public access to sensitive objects.

---

## Conclusion
By following this guide, you can create an S3 bucket with versioning and configure it for public access in a secure manner. Regularly monitor access and apply best practices to ensure data security and cost efficiency.

---



