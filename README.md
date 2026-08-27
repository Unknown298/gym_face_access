# 🏋️ GymFace — Serverless Face Recognition Access System

A browser-based gym access control system that verifies member identity using facial recognition, backed by a fully serverless AWS architecture.

## Overview

GymFace lets a gym front-desk (or a self-service kiosk) verify member access or register new members using just a webcam — no physical access cards or manual check-ins required. A member's face is captured directly in the browser, sent to a serverless backend for facial recognition matching, and access is granted or denied in real time based on membership status.

## How It Works

1. **Register Member** — Front desk captures a new member's face via webcam, along with their name, membership type (Basic/Premium), and expiry date. This is sent to the backend, which stores the face data and member details.
2. **Verify Access** — A returning member's face is captured and sent to the backend, which runs facial recognition against registered members. Access is granted if a match is found and the membership is active; denied otherwise, with a reason (e.g. expired membership, no match found).

## Architecture

- **Frontend:** Single-page HTML/CSS/JavaScript app — uses the browser's `getUserMedia` API to access the webcam, captures frames to a canvas, and converts them to base64 for transmission.
- **API Layer:** AWS API Gateway exposing `/verify` and `/register` REST endpoints.
- **Compute:** AWS Lambda functions handle registration and verification logic.
- **Facial Recognition:** AWS Rekognition for face matching against registered members.
- **Storage:** AWS DynamoDB for member records (name, membership type, expiry, face data reference); AWS S3 for storing captured face images.

```
Browser (camera capture) 
    → API Gateway 
        → Lambda (register / verify logic)
            → Rekognition (face matching)
            → DynamoDB (member records)
            → S3 (face image storage)
```

## Tech Stack

`HTML` `CSS` `JavaScript` `AWS Lambda` `AWS API Gateway` `AWS Rekognition` `AWS DynamoDB` `AWS S3`

## Project Status

The frontend is fully functional and demonstrates the complete user flow (camera capture, registration form, verification flow, result states). The AWS backend (Lambda/API Gateway/DynamoDB) was built and tested during development but the AWS account resources are currently inactive, so live API calls are not available in this demo. The UI can still be opened and walked through to demonstrate the intended user experience and interaction flow.

## Key Learnings

- Building a fully serverless pipeline (API Gateway → Lambda → Rekognition → DynamoDB) without managing any servers
- Handling browser camera access and image capture using the `MediaDevices` API and HTML Canvas
- Designing a REST API contract between a static frontend and serverless backend
- Structuring async fetch calls with proper error handling and user-facing status states (granted/denied/info)

## Running Locally

Since this is a static frontend, simply open `index.html` in a browser. Note: the API calls to `/verify` and `/register` require the backend AWS resources to be active — see Project Status above.
