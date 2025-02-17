# Project Structure: Tiger Anti-Pattern Detection

## **Directory Structure Overview**
The **Tiger Anti-Pattern Detection** project follows a **monorepo structure**, keeping all components (frontend, backend, and machine learning pipeline) in a single repository. This approach ensures a unified development workflow, easier dependency management, and consistent versioning.

### **Directory Layout**
```
/tiger-anti-pattern-detection
│── /frontend              # Next.js React application
│   │── /components        # Reusable UI components
│   │── /pages             # Next.js routes (e.g., dashboard, upload, training)
│   │── /styles            # Global styles
│   │── /utils             # Helper functions
│   │── /services          # API calls to Amplify Data and Rekognition
│
│── /backend               # AWS Amplify backend
│   │── /graphql           # GraphQL schemas and resolvers
│   │── /functions         # AWS Lambda functions
│   │── /auth              # Authentication logic using Cognito
│
│── /ml-pipeline           # Machine Learning model processing
│   │── /training          # Model training scripts
│   │── /inference         # Model inference logic
│   │── /data-prep         # Data preprocessing and transformation
│
│── /config                # Configuration files
│── /docs                  # Project documentation
│── README.md              # Project summary
│── package.json           # Dependencies and scripts
│── .gitignore             # Git ignore rules
```

## **Directory Breakdown**

### **Frontend**
- **`/components`**: Reusable UI components (e.g., VideoPlayer, AnnotationTool).
- **`/pages`**: Next.js pages (e.g., `/dashboard`, `/upload`, `/train-model`).
- **`/styles`**: TailwindCSS for styling.
- **`/utils`**: Utility functions for formatting and calculations.
- **`/services`**: API service layer for interactions with AWS Amplify.

### **Backend**
- **`/graphql`**: Amplify GraphQL API schema definitions.
- **`/functions`**: AWS Lambda functions for video processing and model inference.
- **`/auth`**: User authentication and role management.

### **Machine Learning Pipeline**
- **`/training`**: Scripts for AWS Rekognition Custom Labels model training.
- **`/inference`**: Functions for running inference on test videos.
- **`/data-prep`**: Data cleaning and formatting utilities.

### **Docs & Config**
- **`/docs`**: Project documentation.
- **`/config`**: Configuration settings for cloud services.

## **Rationale for Monorepo Approach**
- Ensures **tight integration** between frontend, backend, and ML components.
- Simplifies **dependency management** with a single package.json.
- Easier **collaboration and versioning** across all project parts.

This structure provides **modularity, scalability, and maintainability**, ensuring an efficient development and deployment process for the Tiger Anti-Pattern Detection project.

