# Technology Stack for Tiger Anti-Pattern Detection

## **Frontend**
### **Framework: Next.js (React) with TypeScript**
- **Why?**
  - Supports both **client-side** and **server-side rendering** for optimized performance.
  - **TypeScript** ensures type safety and maintainability.
  - Rich ecosystem with libraries like **React Query** for data fetching.

### **UI Library: Tailwind CSS**
- **Why?**
  - Utility-first approach for rapid UI development.
  - Highly customizable and efficient styling.

### **State Management: React Context API + React Query**
- **Why?**
  - **Context API** for global state management without excessive boilerplate.
  - **React Query** for caching and synchronizing server state.

---

## **Backend**
### **Framework: AWS Amplify (GraphQL + Lambda)**
- **Why?**
  - Provides a fully managed GraphQL API with **Amplify Data**.
  - Supports AWS Lambda for custom business logic.

### **Database: AWS Amplify Data (DynamoDB-backed GraphQL API)**
- **Why?**
  - Scalable, NoSQL backend with real-time data synchronization.
  - Seamless integration with the Amplify GraphQL API.

### **Authentication: AWS Amplify Auth (Cognito)**
- **Why?**
  - Provides secure, scalable authentication with role-based access control.
  - Supports social login, multi-factor authentication (MFA).

---

## **Machine Learning**
### **Framework: AWS Rekognition Custom Labels**
- **Why?**
  - Provides AI-driven object detection and event classification.
  - Trains models with annotated data for anti-pattern detection.

### **Data Annotation: SageMaker Ground Truth**
- **Why?**
  - Provides industry-standard dataset labeling tools.
  - Supports bounding box annotations and human-in-the-loop corrections.

### **Inference Pipeline: AWS Lambda + Rekognition API**
- **Why?**
  - Lambda functions handle video frame extraction and send them to Rekognition for inference.

---

## **Storage & Media Processing**
### **File Storage: Amazon S3**
- **Why?**
  - Secure, scalable storage for video recordings and extracted frames.
  - Integration with AWS Rekognition for real-time processing.

### **Video Processing: FFmpeg (Lambda Function)**
- **Why?**
  - Used for extracting frames at specific timestamps for annotation.
  - Converts and resizes video files for efficient processing.

---

## **Event Notifications & Messaging**
### **Service: AWS SNS (Simple Notification Service)**
- **Why?**
  - Sends real-time notifications when model training is completed.

### **Real-time Event Handling: AWS EventBridge**
- **Why?**
  - Streams event logs from video analysis into real-time dashboards.

---

## **Development & Deployment**
### **Version Control: GitHub**
- **Why?**
  - Hosted Git repository for source code management.
  - Supports CI/CD workflows.

### **CI/CD: AWS Amplify Hosting & GitHub Actions**
- **Why?**
  - Automates build and deployment for frontend/backend.
  - Provides staging environments for testing before production rollout.

This technology stack ensures that **Tiger Anti-Pattern Detection** is **scalable, efficient, and cloud-native**, leveraging AWS services for AI-driven video analysis and a modern frontend stack for user interaction.

