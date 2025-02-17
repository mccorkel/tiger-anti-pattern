# Implementation Details of Tiger Anti-Pattern Detection

## **Development Approach**
The **Tiger Anti-Pattern Detection** project follows an **Agile development methodology**, ensuring incremental improvements and continuous user feedback. The application is structured as a **Next.js React app** hosted on **AWS Amplify Gen 2** for scalability and ease of deployment. The backend is managed using **AWS Amplify Data**, while machine learning processes rely on **AWS Rekognition Custom Labels**.

## **Coding Standards**
- **Frontend:** Next.js with **TypeScript** for type safety and maintainability.
- **Backend:** Uses **AWS Amplify Data** (GraphQL API) and AWS Lambda for additional business logic.
- **Version Control:** Git-based workflow with feature branching, hosted on **GitHub**.
- **Linting & Formatting:** Enforced with **ESLint & Prettier**.
- **Testing:** Unit tests with **Jest**, integration tests using **Cypress**.

## **Timeline Estimates**
### **Phase 1: Setup & Core Development (Weeks 1-4)**
- Set up Next.js project and AWS Amplify backend.
- Define GraphQL schema for Amplify Data.
- Implement user authentication with Cognito.

### **Phase 2: Training Data & Annotation UI (Weeks 5-8)**
- Develop UI for video annotation (frame extraction, bounding box drawing).
- Enable automatic loading of annotations, timestamps, and categories from uploaded spreadsheets.
- Implement storage of labeled images in SageMaker Ground Truth format.

### **Phase 3: Model Training & Validation (Weeks 9-12)**
- Enable dataset creation and AWS Rekognition Custom Labels training.
- Develop validation pipeline for running model inference on annotated videos.
- Compare model predictions with ground-truth annotations and calculate accuracy metrics.

### **Phase 4: Finalization & Optimization (Weeks 13-16)**
- Refine UI/UX based on user feedback.
- Optimize database queries for faster performance.
- Conduct thorough end-to-end testing and deploy to production.

## **Technical Guidelines**
- **Amplify Data:** Used as a backend service with GraphQL APIs for structured storage.
- **AWS Rekognition Custom Labels:** Handles model training and inference.
- **AWS SNS:** Notifies users when model training is completed.
- **AWS Lambda:** Processes video frames and applies ML models for classification.
- **Amazon S3:** Stores video segments and extracted frames for annotation and model training.

## **Framework Specifics**
### **Frontend (Next.js & React)**
- Client-side and server-side rendering for optimized performance.
- Uses **React Query** for efficient data fetching.

### **Backend (AWS Amplify & GraphQL)**
- Provides structured storage and real-time updates.
- Integrates seamlessly with Cognito for user authentication.

### **Machine Learning (AWS Rekognition & SageMaker)**
- Custom ML model training using annotated datasets.
- Image and video analysis for detecting predefined behaviors.

## **Database Design**
The **Tiger Anti-Pattern Detection** project uses **AWS Amplify Data** (DynamoDB-backed GraphQL API) to store structured records:

- **UserProfile** (Tracks registered users and roles)
- **TrainingDataEntry** (Stores uploaded training data and annotations)
- **AnnotatedImage** (Stores frame snapshots with bounding boxes)
- **Dataset** (Groups training images into datasets for ML models)
- **ModelTrainingJob** (Tracks AWS Rekognition Custom Labels training jobs)
- **ModelInferenceResult** (Stores test images and model output labels)
- **ModelPerformance** (Tracks accuracy metrics from validation tests)

## **Cloud Services Used**
| **Service** | **Purpose** |
|------------|-------------|
| **AWS Amplify** | Hosting, backend GraphQL API, authentication |
| **Amazon S3** | Storage for video files and extracted frames |
| **AWS Lambda** | Processes images and integrates with Rekognition |
| **AWS Rekognition** | AI model training and inference for detecting patterns |
| **AWS SNS** | Sends notifications for model training completion |

This implementation plan ensures an **efficient, scalable, and cloud-native** solution for detecting anti-patterns in educational videos.

