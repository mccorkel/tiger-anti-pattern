# User Flow for Tiger Anti-Pattern Detection

## **1. User Registration & Login**
### **Flow:**
1. User visits the **login page**.
2. If the user has an account, they log in using **AWS Cognito authentication**.
3. If the user does not have an account, they go through the **registration process**.
4. Upon successful authentication, the user is redirected to the **dashboard**.

### **Edge Cases:**
- Incorrect credentials → Show an error message.
- Expired session → Redirect to login.
- First-time login → Prompt user to complete profile information.

---

## **2. Dashboard Interaction**
### **Flow:**
1. After login, users land on the **dashboard**.
2. The dashboard displays:
   - Recent **training data entries**.
   - Recent **validation results**.
   - Quick actions (**Upload Spreadsheet, Train Model, Run Model Validation, Test Model**).
3. Users can select an action or browse recent entries.

### **Edge Cases:**
- No training data uploaded yet → Show an empty state with guidance.
- No validation results available → Prompt the user to run a validation.

---

## **3. Uploading a Spreadsheet (Training or Validation)**
### **Flow:**
1. User clicks **"Upload Spreadsheet"** from the dashboard.
2. User selects a file and uploads it.
3. A prompt asks whether the file is for **training** or **validation**.
4. The system processes the file and stores it accordingly:
   - **Training:** Extracts frames for annotation.
   - **Validation:** Runs videos through a trained model and generates accuracy reports.

### **Edge Cases:**
- Incorrect file format → Show an error message.
- Large file upload → Display progress indicator.

---

## **4. Annotating Training Data**
### **Flow:**
1. User selects a **training data entry** from the list.
2. The system **automatically loads annotations, timestamps, and event categories**.
3. User can **adjust timestamps if necessary**.
4. User draws **bounding boxes** on relevant areas of the frame.
5. The system saves the annotation in **SageMaker Ground Truth format** and uploads it to **S3**.

### **Edge Cases:**
- User selects an incorrect timestamp → Allow adjustments.
- User forgets to draw bounding boxes → Show a validation prompt.

---

## **5. Running Model Validation**
### **Flow:**
1. User selects a **validation spreadsheet**.
2. The system runs videos through a **trained AWS Rekognition Custom Labels model**.
3. Detected labels are compared against ground-truth annotations.
4. The system generates **precision, recall, and F1-score metrics**.
5. The results are displayed on the **Validation Results page**.

### **Edge Cases:**
- Model fails to detect labels → Show confidence scores and allow review.
- Validation data mismatches → Highlight discrepancies for manual review.

---

## **6. Training a New Model**
### **Flow:**
1. User navigates to the **Train Model** page.
2. The user selects a dataset of annotated images.
3. The system submits a **model training job** to AWS Rekognition.
4. Training runs asynchronously (can take up to 24 hours).
5. Once training completes, the user receives an **AWS SNS notification**.
6. The newly trained model appears in the **Model List**.

### **Edge Cases:**
- Dataset is incomplete → Prompt the user to add more labeled data.
- Training failure → Show AWS Rekognition error messages.

---

## **7. Testing a Model with an Image**
### **Flow:**
1. User navigates to the **Test Model** page.
2. The user uploads an image for testing.
3. The selected trained model processes the image.
4. The system returns detected labels with confidence scores.

### **Edge Cases:**
- Model confidence too low → Provide suggestions for retraining.
- Image format not supported → Display error message.

---

## **8. Admin User Management**
### **Flow:**
1. Admin navigates to the **User Management** page.
2. Admin sees a list of registered users.
3. Admin can:
   - Promote/demote users as **admins**.
   - Remove users.
   - View user activity logs.

### **Edge Cases:**
- Unauthorized users trying to access → Redirect to dashboard.
- Admin accidentally demotes themselves → Prevent from removing own admin role.

---

This user flow ensures a smooth experience, guiding users through **data annotation, model training, validation, and testing**, while ensuring **secure user management** for admins.

