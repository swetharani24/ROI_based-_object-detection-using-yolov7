
🎯 ROI-Based Object Detection & Segmentation Pipeline

A high-performance real-time computer vision system that combines YOLOv7, OpenCV, RabbitMQ, and Redis to perform Object Detection, Segmentation, and ROI-Based Event Filtering. The distributed architecture enables scalable, low-latency processing for industrial and surveillance applications.

📌 Table of Contents
Overview
Features
System Architecture
Workflow
Redis Integration
RabbitMQ Integration
ROI Processing
Threading Architecture
Project Structure
Technologies Used
Applications
Future Enhancements
📖 Overview

The application captures video frames continuously, stores them temporarily in Redis, and publishes Frame IDs through RabbitMQ. Dedicated workers perform Object Detection and Segmentation independently. Detection results are again published to RabbitMQ, where an ROI Processor validates whether the detected object lies inside the predefined Region of Interest.

Only valid ROI detections are stored and displayed.

This architecture significantly improves performance by separating frame storage, processing, and communication.

✨ Features
🎥 Real-Time Video Processing
🎯 ROI-Based Object Filtering
🤖 YOLOv7 Object Detection
🖼️ Image Segmentation
📦 RabbitMQ Message Queues
🗄️ Redis Frame Storage
🧵 Multi-Threaded Processing
📊 Object Counting
⚡ High Throughput
🚀 Modular & Scalable Design
🛠️ Technologies Used
Technology	Purpose
Python	Core Programming
OpenCV	Video Processing
YOLOv7	Object Detection
PyTorch	Deep Learning Framework
Redis	Frame Storage
RabbitMQ	Message Queue
NumPy	Numerical Operations
Threading	Parallel Processing
⚙️ Complete Workflow
1️⃣ Frame Capture
Capture frames continuously from a live camera or video.
Assign a unique Frame ID.
2️⃣ Store Frames in Redis

Instead of transferring images between modules, each captured frame is stored in Redis.

Example Redis Keys

vehicle_frames
safety_frames

Redis provides:

High-speed in-memory storage
Shared frame access
Low latency
Reduced memory duplication
3️⃣ RabbitMQ Exchange

Only lightweight metadata is sent through RabbitMQ.

Example Message

{
  "frame_id": 102,
  "camera_id": 1,
  "timestamp": "2026-06-26 12:10:32"
}

Advantages:

Faster communication
Lower network usage
Easy scalability
4️⃣ Detection Processor

Detection Worker performs:

Receive Frame ID
Read frame from Redis
Load YOLOv7 model
Detect objects
Generate bounding boxes
Calculate confidence score
Publish detection results to RabbitMQ

Supported Objects

👤 Person
🚗 Car
🏍 Bike
🦺 Safety Jacket
⛑ Helmet
🔥 Fire
💨 Smoke
5️⃣ Segmentation Processor

Segmentation Worker performs:

Read frame from Redis
Execute segmentation model
Generate object masks
Publish segmentation results
6️⃣ ROI Processor

The ROI Processor receives detection results from RabbitMQ.

Workflow:

Read bounding boxes
Check whether the object lies inside the ROI
Save valid detections
Ignore detections outside the ROI

Only ROI detections are considered final.
🧵 Threading Architecture

The system uses independent threads for maximum throughput.

🎥 Frame Capture Thread
🗄 Redis Storage Thread
🤖 Detection Thread
🖼 Segmentation Thread
🎯 ROI Processing Thread
🖥 Display Thread
Benefits
Parallel execution
Better CPU utilization
Faster FPS
Reduced latency
Non-blocking processing
🌍 Applications
🏭 Industrial Safety Monitoring
🚦 Smart Traffic Systems
🚗 Parking Management
🛡 Security Surveillance
📦 Warehouse Automation
🚧 Restricted Area Monitoring
🔥 Fire & Smoke Detection
📈 Future Enhancements
Multi-Camera Support
Dynamic ROI Selection
ByteTrack / DeepSORT Integration
Event Notification System
Dashboard & Analytics
Cloud Deployment
REST API
Database Logging
