# AWS Lambda + S3 + Polly Text-to-Speech + Rekognition Image Tagging

This project converts text files stored in Amazon S3 into audio files using Amazon Polly  
**and** automatically tags images using Amazon Rekognition.  
No Comprehend is used — only Lambda, S3, Polly, and Rekognition.

---

## 📂 Project Structure

We use three S3 folders (prefixes):

- **`input/`** — Place `.txt` files here for processing.
- **`audio/`** — Generated `.mp3` files are saved here.
- **`images/`** — Place image files here for tagging.

---

## ⚙️ How It Works

### **Text-to-Speech Workflow**
1. Upload a `.txt` file to the `input/` folder in S3.
2. An **S3 event trigger** invokes an AWS Lambda function.
3. Lambda:
   - Reads the text from the file.
   - Sends the text to **Amazon Polly**.
   - Receives the audio output (MP3 format).
   - Saves the MP3 file to the `audio/` folder in the same S3 bucket.
4. The audio file can then be downloaded or streamed.

### **Image Tagging Workflow**
1. Upload an image (`.jpg`, `.png`, etc.) to the `images/` folder in S3.
2. An **S3 event trigger** invokes the same Lambda function (or a separate one if preferred).
3. Lambda:
   - Calls **Amazon Rekognition** to detect labels (objects, scenes, concepts) in the image.
   - Saves the tags as a `.json` file to the `images/` folder or another folder (e.g., `tags/`).
4. The JSON file contains detected labels with confidence scores.

---

## 🛠️ Setup Steps

### 1. Create an S3 Bucket
- Create a new bucket (e.g., `my-aws-processing-bucket`).
- Inside the bucket, create three folders:  
  - `input/`  
  - `audio/`  
  - `images/`

### 2. Create the Lambda Function
- Runtime: **Python 3.x** (or Node.js if preferred).
- Attach the following IAM permissions:
  - `AmazonS3ReadOnlyAccess` (read input and image files)
  - `AmazonS3FullAccess` (to write audio and JSON tag files — or restrict by prefix)
  - `AmazonPollyFullAccess` (to synthesize speech)
  - `AmazonRekognitionReadOnlyAccess` (to detect image labels)
- Add **two S3 triggers**:
  - Trigger 1: For `.txt` files in `input/` (runs Polly workflow).
  - Trigger 2: For image files in `images/` (runs Rekognition workflow).

### 3. Paste Lambda Code

📷 **Example Workflows**
- **Text-to-Speech:**
  1. Upload: `input/example.txt`
  2. Lambda → Polly → Save
  3. Output: `audio/example.mp3` in S3

- **Image Tagging:**
  1. Upload: `images/photo.jpg`
  2. Lambda → Rekognition → Save tags
  3. Output: `images/photo-tags.json` in S3

