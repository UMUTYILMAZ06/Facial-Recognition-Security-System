Real-Time Suspect Identification with Gender & Facial Hair Classification using CNN and DeepFace
📌 Project Overview
This project was developed within the scope of a Big Data course to simulate a real-time suspect identification system. The system combines deep learning, cloud storage, and stream processing to detect and analyze human faces captured from live video input and to share critical information with law enforcement authorities.

🚀 Key Features
Real-time face detection using a laptop camera

Gender classification (Male / Female) with a CNN model

Facial hair (goatee) classification among males

Cloud storage of results and embedded vectors (Azure Blob Storage)

Face embedding generation using Google DeepFace (VGG-Face model)

Suspect tracking using image similarity and temporal co-occurrence

Graph/tree construction of co-presence relationships (friendship trees)

Real-time message delivery with Apache Kafka

Remote consumer setup via AWS EC2 Virtual Machine

🧠 Technologies Used
Category	Tools/Frameworks
Deep Learning	TensorFlow / Keras, CNN, DeepFace
Cloud Storage	Azure Blob Storage
Real-time Messaging	Apache Kafka (Producer/Consumer)
Face Embedding	DeepFace - VGG-Face Model
Frontend Source	Webcam via OpenCV
Backend Stream Logic	Python Kafka Client
Remote Consumer Infra	AWS EC2 Linux instance (for Emniyet/Police Simulation)

📷 Step 1: Face Capture & Prediction
Webcam is activated via OpenCV.

Faces are detected using Haar cascade.

Detected faces are passed through:

A CNN Gender Classification Model

A CNN Goatee Classification Model (only for males)

🔍 Step 2: Embedding & Cloud Storage
For each detected face, DeepFace is used to generate a 128D vector embedding.

These embeddings are:

Stored in lightweight CSV format

Uploaded to Azure Blob Storage for permanent access

Mapped to corresponding attributes (e.g., gender, goatee, image_id)

🌳 Step 3: Suspicion Detection & Co-Presence Analysis
Given a suspect image, the system can:

Find similar individuals from stored embeddings

Retrieve a list of individuals who entered the same space (e.g., mall) concurrently

Co-occurrence is stored as a Friendship Tree, which is streamed for real-time access.

📡 Step 4: Real-Time Kafka Streaming
The final tree and suspect data are:

Published as Kafka messages via a Python Kafka Producer

Streamed to AWS-hosted Kafka Consumers (simulating police infrastructure)

Consumers are continuously running and listen for updates in real-time.

🧪 How to Run the System
1. Face Capture & CNN Prediction
bash
Kopyala
Düzenle
python app.py
2. Kafka Producer (Send Tree)
bash

python kafka_producer.py
3. Kafka Consumer (Police Receiver on AWS)
bash

python kafka_consumer.py
🗃️ Folder Structure
graphql
Kopyala
Düzenle
project-root/
│
├── app.py                         # Face capture and CNN prediction
├── gender_model.h5               # Trained gender classification model
├── goatee_model.h5               # Trained facial hair model
├── kafka_producer.py            # Sends data to Kafka
├── kafka_consumer.py            # Receives and logs data from Kafka
├── embeddings/                   # Contains generated DeepFace vectors
├── cloud_utils.py               # Azure Blob interaction helper
├── friendship_tree.py           # Builds co-occurrence tree from data
├── final_merged_code_trial2.ipynb # Full integrated workflow
🔐 Use Case: Suspect Identification in Malls
This system is designed to assist in:

Identifying a suspect from a new photo using embedding similarity

Listing all individuals who entered the same mall at the same time

Providing the friendship tree of people associated with a suspect

Streaming this data securely to police infrastructure in real time

💡 Future Enhancements
Integration with surveillance camera feeds

Use of facial recognition for cross-camera tracking

More advanced face attribute models (age, emotion)

Privacy-aware logging and access control

Developed by Umut Yılmaz, Fuad Saffedoğlu, Emre Şahin Demirbaş
Çankaya University —
