# Realtime Translator

**Realtime Translator** is an AWS Lambda + API Gateway project for real-time text translation using Amazon Translate.

## Features
- Receives text from the user in JSON format.  
- Translates text to any target language (`target`).  
- Returns a JSON response with the translated text.  
- Fully serverless, hosted on AWS.

## Requirements
- Active AWS account.  
- Lambda and Amazon Translate permissions.  
- Python 3.12 (for the Lambda function).  

## Architecture
- **Lambda Function**: contains the code to receive JSON input and call Amazon Translate.  
- **API Gateway**: provides the HTTP endpoint to connect Lambda to the internet.  
- **CORS**: enabled to allow browser-based testing.

## How to Use
1. Send a POST request to the API:
```bash
curl -X POST "https://<api-id>.execute-api.<region>.amazonaws.com/prod/radwantranslatefunc" \
-H "Content-Type: application/json" \
-d '{"text": "Hello world", "target": "de"}'
