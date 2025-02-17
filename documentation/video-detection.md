# Video Detection Engine - Tiger Anti-Pattern Detection

## **Architecture Overview**
The **Video Detection Engine** processes live video streams in real-time using **WebRTC**, **AWS Kinesis Video Streams**, **AWS Rekognition Custom Labels**, and **AWS EventBridge**. This enables **low-latency detection and event broadcasting** to multiple applications.

### **Workflow:**
1. **WebRTC Streaming → Kinesis Video Streams**
   - A WebRTC client (browser/native app) captures and streams live video to **AWS Kinesis Video Streams**.
   - Kinesis temporarily stores the video and makes it available for real-time analysis.

2. **AWS Rekognition Custom Labels → Real-time Inference**
   - AWS Rekognition Custom Labels is connected to **Kinesis Video Streams**.
   - Rekognition analyzes incoming video frames and detects **predefined labels** (e.g., "CHEATING", "AWAY_FROM_SEAT").

3. **SNS Notifications for Detected Events**
   - When **Rekognition detects an event**, it **sends an SNS notification**.
   - The notification includes **event type, confidence score, timestamp, and bounding boxes (if applicable).**

4. **AWS EventBridge for Broadcasting Events**
   - **AWS EventBridge subscribes to the SNS topic.**
   - It **forwards detection events** to various consumers, such as:
     - **Databases** (store detections for historical analysis)
     - **Frontend apps** (real-time UI updates)
     - **Monitoring dashboards** (event logs for administrators)
     - **Third-party apps** (integrating detection into external systems)

---

## **Advantages of This Architecture**
✅ **Real-time event detection** – WebRTC ensures **low-latency streaming**, and Rekognition processes frames **in near real-time**.  
✅ **Scalability** – Kinesis Video Streams can **handle multiple concurrent video feeds**.  
✅ **Event-driven architecture** – EventBridge allows **multiple systems to subscribe** without tight coupling.  
✅ **Cross-platform notifications** – Apps can subscribe to **EventBridge event buses** via WebSockets, Webhooks, or API Gateway.  

---

## **Steps to Implement**
### **1. Set Up WebRTC Streaming**
- Implement a **WebRTC client** to capture video and send it to **Kinesis Video Streams**.
- Use **Amazon Kinesis Video Streams WebRTC SDK** for native or browser-based implementations.

### **2. Configure Kinesis Video Streams**
- Create a **Kinesis Video Stream** in AWS.
- Ensure Rekognition has **read access** to the Kinesis stream.

### **3. Connect AWS Rekognition Custom Labels**
- Train a **Custom Labels model** in AWS Rekognition.
- Attach the trained model to **Kinesis Video Streams** for inference.

### **4. Enable SNS Notifications**
- Create an **SNS topic** to receive Rekognition event notifications.
- Subscribe EventBridge to this SNS topic.

### **5. Configure AWS EventBridge for Broadcasting**
- Set up an **EventBridge rule** that listens for SNS notifications.
- Define multiple **targets** (e.g., databases, frontends, dashboards, third-party apps).

### **6. Develop Event Consumers**
- Implement **WebSockets, Webhooks, or API Gateway** to relay events to apps.
- Store events in a **database** for later review and analytics.

---

## **Detailed Architecture Diagram**

```plaintext
[ WebRTC Client ] → [ Kinesis Video Streams ] → [ AWS Rekognition Custom Labels ] → [ SNS Notification ] → [ EventBridge ] → [ Multiple Consumers ]
```

---

## **Sample AWS CloudFormation Setup**

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  KinesisVideoStream:
    Type: AWS::KinesisVideo::Stream
    Properties:
      DataRetentionInHours: 24
      MediaType: "video/h264"
      Name: "TigerDetectionStream"

  RekognitionStreamProcessor:
    Type: AWS::Rekognition::StreamProcessor
    Properties:
      Name: "TigerRekognitionProcessor"
      KinesisVideoStream:
        Arn: !GetAtt KinesisVideoStream.Arn
      RoleArn: "arn:aws:iam::123456789012:role/RekognitionAccess"
      NotificationChannel:
        SNSTopicArn: !Ref SNSTopic
      RegionsOfInterest:
        - BoundingBox:
            Width: 0.5
            Height: 0.5
            Left: 0.25
            Top: 0.25

  SNSTopic:
    Type: AWS::SNS::Topic
    Properties:
      DisplayName: "TigerDetectionSNS"

  EventBridgeRule:
    Type: AWS::Events::Rule
    Properties:
      EventPattern:
        source:
          - "aws.rekognition"
      Targets:
        - Arn: "arn:aws:lambda:us-east-1:123456789012:function:ProcessRekognitionEvent"
          Id: "RekognitionEventTarget"

```

---

## **Next Steps**
1. Deploy the **Kinesis Video Stream** and integrate **WebRTC streaming**.
2. Train and deploy a **Rekognition Custom Labels model**.
3. Implement **SNS + EventBridge integration**.
4. Develop event consumers (frontend dashboards, monitoring tools, databases).

This setup ensures a **real-time, scalable, and event-driven** architecture for the **Tiger Anti-Pattern Detection** Video Detection Engine.