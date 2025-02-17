# Requirements for Tiger Anti-Pattern Detection

## **Functional Requirements**
1. **User Authentication & Role Management**
   - Users must be able to sign in and manage their accounts via AWS Cognito.
   - Admin users should have permission to approve, reject, or modify training data.
   - Only authenticated users can access protected routes.

2. **Training Data Annotation**
   - Users should be able to upload and review training videos.
   - Automatically load annotations, timespans, timestamps, and categories from uploaded spreadsheets.
   - Users must be able to adjust timestamps and define event labels from a dropdown list.
   - Users should be able to draw bounding boxes around relevant areas in video frames.
   - Save annotations in AWS SageMaker Ground Truth format and store them in S3.

3. **Model Training & Management**
   - Users can create and manage datasets for AWS Rekognition Custom Labels.
   - Allow users to initiate model training asynchronously.
   - Notify users via AWS SNS when model training is completed.

4. **Model Validation & Performance Tracking**
   - Users can test trained models against validation datasets.
   - Detected labels should be compared against ground-truth annotations.
   - Generate accuracy reports including precision, recall, and F1-score.
   - Store validation results and allow users to review model performance over time.

5. **Event & Behavior Tracking**
   - Detect and log anti-pattern events (e.g., IDLING, AWAY_FROM_SEAT, CHEATING).
   - Support real-time and batch processing of video feeds.
   
## **Non-Functional Requirements**

### **Performance**
- The system should support **real-time video processing** with latency under **5 seconds**.
- Training data should be **retrievable within seconds** for user review.
- Model inference should return results **within 2 seconds** for single-frame analysis.

### **Scalability**
- Must handle **thousands of concurrent users and video streams**.
- S3 should support **large datasets** without performance degradation.
- AWS Rekognition must scale dynamically to support increased demand.

### **Security**
- User data and annotations must be encrypted at rest and in transit.
- Access control should be **role-based (Admin, Reviewer, Annotator)**.
- Only approved users can modify training datasets.

### **Usability**
- Web UI should be **intuitive and responsive across devices**.
- Annotation tools should provide **real-time feedback** for bounding boxes.
- Users should be guided through workflows with **tooltips and validation messages**.

### **Maintainability**
- Codebase should be **modular**, using **Next.js best practices**.
- API contracts should be documented with **GraphQL schemas**.
- System should support easy deployment and rollback via **AWS Amplify CI/CD**.

This requirements document ensures that **Tiger Anti-Pattern Detection** is **functional, scalable, and secure**, supporting real-time AI-driven video analysis for education monitoring.

