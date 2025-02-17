# Features of Tiger Anti-Pattern Detection

## **1. User Authentication & Role Management**
### **Purpose:**
- Secure access to the application, ensuring only authorized users can access training and validation tools.
- Differentiate between **admin users** and **standard users**.

### **Functionality:**
- Users sign in via AWS Cognito authentication.
- Admins can manage user roles (promote/demote users as admins).
- Only authenticated users can access protected routes.

### **Edge Cases:**
- Handling incorrect credentials.
- Expired session handling.
- Preventing admins from removing their own admin status.

### **Business Rules:**
- Only admin users can manage roles.
- Regular users can annotate and validate but cannot modify datasets or models.

### **Validation Requirements:**
- Verify that login credentials are correct.
- Ensure session tokens are valid and not expired.

---

## **2. Dashboard**
### **Purpose:**
- Provide users with a centralized location to view recent activity and access key functionality.

### **Functionality:**
- Displays **recent training data entries**.
- Shows **model validation results**.
- Provides quick actions for **uploading spreadsheets, training models, running validations, and testing models**.

### **Edge Cases:**
- No training data uploaded → Show an empty state with guidance.
- No validation results available → Prompt the user to run a validation.

### **Business Rules:**
- Only authenticated users can access the dashboard.
- Admins see additional admin controls.

### **Validation Requirements:**
- Ensure all data displayed is fetched dynamically and up to date.

---

## **3. Uploading a Spreadsheet (Training or Validation)**
### **Purpose:**
- Allow users to upload a spreadsheet for either training data generation or model validation.

### **Functionality:**
- Users select a file and upload it.
- A prompt asks whether the file is for **training** or **validation**.
- The system processes the file accordingly:
  - **Training:** Extracts frames for annotation.
  - **Validation:** Runs videos through the trained model to generate accuracy reports.

### **Edge Cases:**
- Incorrect file format → Show an error message.
- Large file upload → Display progress indicator.

### **Business Rules:**
- Users must select **training or validation** before processing.
- File parsing must check for missing or incorrect values.

### **Validation Requirements:**
- Ensure the uploaded file has valid data.
- Validate file format before processing.

---

## **4. Annotating Training Data**
### **Purpose:**
- Allow users to review and adjust training data, ensuring accurate event labels and bounding boxes.

### **Functionality:**
- Users select a training data entry from the list.
- The system **automatically loads annotations, timestamps, and event categories**.
- Users can adjust timestamps if necessary.
- Users draw bounding boxes on relevant areas of the frame.
- The system saves the annotation in **SageMaker Ground Truth format** and uploads it to **S3**.

### **Edge Cases:**
- Users select incorrect timestamps → Allow adjustments.
- Users forget to draw bounding boxes → Show a validation prompt.

### **Business Rules:**
- Only users with the correct permissions can annotate data.
- Bounding boxes must be drawn before saving an entry.

### **Validation Requirements:**
- Ensure timestamps align with video duration.
- Validate bounding boxes before submission.

---

## **5. Running Model Validation**
### **Purpose:**
- Validate an existing trained model by running test videos through it and comparing predictions to ground truth annotations.

### **Functionality:**
- Users select a **validation spreadsheet**.
- The system runs videos through an **AWS Rekognition Custom Labels model**.
- Detected labels are compared against ground truth annotations.
- The system generates **precision, recall, and F1-score metrics**.
- The results are displayed on the **Validation Results page**.

### **Edge Cases:**
- Model fails to detect labels → Show confidence scores and allow review.
- Validation data mismatches → Highlight discrepancies for manual review.

### **Business Rules:**
- Only authenticated users can run validations.
- Users must upload correctly formatted validation spreadsheets.

### **Validation Requirements:**
- Cross-check detected events against ground-truth annotations.
- Ensure calculations for precision, recall, and F1-score are correct.

---

## **6. Training a New Model**
### **Purpose:**
- Allow users to train a new AWS Rekognition model based on annotated datasets.

### **Functionality:**
- Users select an existing dataset.
- The system submits a **training job** to AWS Rekognition Custom Labels.
- Training runs asynchronously (can take up to 24 hours).
- Users receive an **AWS SNS notification** when training completes.
- The newly trained model appears in the **Model List**.

### **Edge Cases:**
- Dataset is incomplete → Prompt user to add more labeled data.
- Training failure → Show AWS Rekognition error messages.

### **Business Rules:**
- Only users with admin permissions can train new models.
- Dataset must have a minimum number of annotated images.

### **Validation Requirements:**
- Ensure dataset meets size requirements before training.
- Monitor training status and send completion notifications.

---

## **7. Testing a Model with an Image**
### **Purpose:**
- Allow users to run inference on a trained model using an uploaded image.

### **Functionality:**
- Users upload an image.
- The selected trained model processes the image.
- The system returns detected labels with confidence scores.

### **Edge Cases:**
- Model confidence too low → Provide suggestions for retraining.
- Image format not supported → Display error message.

### **Business Rules:**
- Only authenticated users can test models.

### **Validation Requirements:**
- Validate uploaded image format before processing.

---

## **8. Admin User Management**
### **Purpose:**
- Allow admins to manage user roles and permissions.

### **Functionality:**
- Admins can view registered users.
- Admins can **promote/demote users as admins**.
- Admins can remove users.
- Admins can view user activity logs.

### **Edge Cases:**
- Unauthorized users trying to access → Redirect to dashboard.
- Admin accidentally demotes themselves → Prevent from removing own admin role.

### **Business Rules:**
- Only admins can modify user roles.

### **Validation Requirements:**
- Ensure role changes are reflected in the database.
- Prevent unauthorized access to admin features.

---

This document outlines the key functionalities, business rules, and validation requirements for each feature in the **Tiger Anti-Pattern Detection** application, ensuring a structured and robust implementation.

