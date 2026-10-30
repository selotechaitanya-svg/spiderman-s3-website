# 🕷️ Amazon S3 Static Website Hosting: Spider-Man Theme

This guide walks you through deploying the Spider-Man static website on Amazon Web Services (AWS) S3, fulfilling all primary requirements, the bonus versioning task, and generating the submission document (DOC/PDF).

---

## 📁 Included Project Files

Located in `spiderman-s3-website/`:
* `index.html`: Responsive, modern Spider-Man themed homepage (NYC incident monitor).
* `404.html`: Custom Spider-Man themed error page ("Web Line Severed").
* `bucket-policy.json`: Amazon S3 public read bucket policy.

---

## 🚀 Step-by-Step AWS Setup Guide

### Step 1: Create an S3 Bucket
1. Log in to the [AWS Management Console](https://console.aws.amazon.com/s3/).
2. Navigate to **S3** and click **Create bucket**.
3. **Bucket name**: Choose a globally unique name (e.g., `spiderman-incident-net-<your-rollno-or-name>`).
4. **AWS Region**: Select your nearest region (e.g., `us-east-1` or `ap-south-1`).
5. **Block Public Access settings for this bucket**:
   - **Uncheck** *"Block all public access"*.
   - Check the acknowledgment box: *"I acknowledge that the current settings might result in this bucket and the objects within becoming public."*
6. Leave other defaults and click **Create bucket**.
📸 *Take Screenshot 1: Bucket created showing general properties.*

---

### Step 2: Enable Static Website Hosting
1. Click on your newly created bucket name.
2. Select the **Properties** tab.
3. Scroll down to the bottom to **Static website hosting** and click **Edit**.
4. Choose **Enable**.
5. **Hosting type**: Select *Host a static website*.
6. **Index document**: Enter `index.html`.
7. **Error document**: Enter `404.html`.
8. Click **Save changes**.
9. Note down the generated **Bucket website endpoint** URL at the bottom:
   `http://<your-bucket-name>.s3-website.<your-region>.amazonaws.com`
📸 *Take Screenshot 2: Static website hosting enabled with index.html & 404.html configured.*

---

### Step 3: Configure Bucket Policy (Public Permissions)
1. In your bucket, select the **Permissions** tab.
2. Scroll to **Bucket policy** and click **Edit**.
3. Copy and paste the policy below (replace `<YOUR_BUCKET_NAME>` with your actual bucket name):
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
    }
  ]
}
```
4. Click **Save changes**. The bucket will now display a red **"Public"** badge.
📸 *Take Screenshot 3: Bucket policy saved and bucket showing 'Publicly accessible'.*

---

### Step 4: Upload Website Files
1. Select the **Objects** tab.
2. Click **Upload** -> **Add files**.
3. Select `index.html` and `404.html` from `spiderman-s3-website/`.
4. Click **Upload**.
📸 *Take Screenshot 4: Objects tab displaying index.html and 404.html.*

---

### Step 5: Verify the Website Endpoints
1. Open your browser and navigate to your bucket website endpoint:
   `http://<your-bucket-name>.s3-website.<your-region>.amazonaws.com`
   *(Verify that the Spider-Man Incident Dispatch Hub homepage renders with full styles).*
   📸 *Take Screenshot 5: Homepage displayed in the browser.*
2. Test the custom error page by appending a non-existent path:
   `http://<your-bucket-name>.s3-website.<your-region>.amazonaws.com/goblin-secret-hideout`
   *(Verify that the custom 404 "Web Line Severed!" page renders).*
   📸 *Take Screenshot 6: Custom 404 error page displayed in the browser.*

---

## 🌟 Bonus Task: S3 Bucket Versioning & Restoration

### 1. Enable Versioning
1. Go to the **Properties** tab of your bucket.
2. Under **Bucket Versioning**, click **Edit**.
3. Select **Enable** and click **Save changes**.
📸 *Take Screenshot 7: Bucket Versioning enabled.*

### 2. Modify `index.html` and Re-upload
1. Open `index.html` and edit the hero banner text or version badge, e.g., change:
   `<h1>Spider-Man Incident Dispatch Hub</h1>`
   to:
   `<h1>Spider-Man Incident Dispatch Hub (v2: Enhanced Defense Grid)</h1>`
2. Save the file.
3. In the S3 Console -> **Objects** tab, click **Upload** and re-upload the modified `index.html`.
4. Visit your website endpoint and refresh to verify the new version is live.

### 3. Demonstrate Versions and Restore
1. In the **Objects** tab, toggle the switch for **"Show versions"** (top right of object list).
2. You will see two versions of `index.html` with distinct **Version IDs** and timestamps.
📸 *Take Screenshot 8: 'Show versions' toggled on displaying multiple versions of index.html.*
3. Select the newest version of `index.html` (the top one) and click **Delete**.
4. Type `delete` to confirm permanent deletion of this version.
5. Refresh your website endpoint in the browser. It will immediately display the original version again!
📸 *Take Screenshot 9: Website displaying the restored original homepage.*

---

## 📝 Justification of Tools and Configurations (For Your Report)

You can include the following explanation in your DOC/PDF report:

> **Architecture & Tool Justification:**
> 1. **Amazon Simple Storage Service (Amazon S3)**: S3 was chosen because it provides a serverless, highly durable (99.999999999% data durability), and cost-efficient hosting environment for static web assets (HTML, CSS, JS, images). It eliminates the overhead, patching, and costs associated with provisioning and managing virtual server instances (EC2).
> 2. **Static Website Hosting Feature**: Built directly into S3, this feature enables automatic request routing, index document delivery (`index.html`), and custom error routing (`404.html`) at high throughput and low latency.
> 3. **Bucket Policy & Public Read Permissions**: By default, S3 buckets block all public ingress for security. For static hosting, we explicitly disable public access block and attach an IAM Bucket Policy allowing `s3:GetObject` actions to `Principal: "*"`. This ensures anonymous web visitors can read assets without having AWS credentials.
> 4. **Amazon S3 Object Versioning**: S3 Versioning preserves every variant of an object stored in the bucket. Enabling versioning guards against accidental overwrites and malicious deletions, allowing rollback to prior releases.

---

## 📋 Final Submission Checklist (DOC / PDF)

Make sure your submitted document includes:
- [ ] **Working S3 Website Endpoint URL**: `http://<bucket-name>.s3-website.<region>.amazonaws.com`
- [ ] **Screenshot 1**: S3 bucket created and static website hosting configuration.
- [ ] **Screenshot 2**: S3 Bucket policy and public access configuration.
- [ ] **Screenshot 3**: S3 Objects tab showing `index.html` and `404.html`.
- [ ] **Screenshot 4**: Working homepage (`index.html`) loaded in the browser.
- [ ] **Screenshot 5**: Custom 404 error page loaded in the browser.
- [ ] **Brief Justification Section**: The text provided above.
- [ ] **Bonus Section**:
  - Screenshot of Bucket Versioning enabled.
  - Screenshot of the S3 Console showing the object version history list.
  - Screenshot of the restored version rendering on the website.
