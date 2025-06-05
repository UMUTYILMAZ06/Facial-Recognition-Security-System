# Real-Time Suspect Identification with Gender & Facial Hair Classification using CNN and DeepFace

## Project Overview

This project was developed as part of a Big Data course to simulate a real-time suspect identification system. The system integrates deep learning, cloud storage, and real-time stream processing to detect and analyze human faces from a live camera feed and share structured data with law enforcement infrastructure.

## Key Features

* Real-time face detection using a laptop webcam.
* Gender classification (Male / Female) using a trained Convolutional Neural Network (CNN) model.
* Facial hair (goatee) classification specifically for male individuals.
* Cloud-based storage of captured face data and their embeddings using Azure Blob Storage.
* Generation of facial embeddings with Google DeepFace (VGG-Face model).
* Retrieval of visually similar individuals for suspect identification.
* Detection of people who entered the same location concurrently (e.g., mall) and construction of a co-occurrence graph (Friendship Tree).
* Real-time message publishing using Apache Kafka.
* Deployment of a Kafka consumer on an AWS EC2 virtual machine representing the police infrastructure for continuous data listening.

## Technologies Used

| Category              | Tools and Frameworks                     |
| --------------------- | ---------------------------------------- |
| Deep Learning         | TensorFlow, Keras, CNN, DeepFace         |
| Face Embedding        | DeepFace (VGG-Face model)                |
| Real-Time Messaging   | Apache Kafka (Producer and Consumer)     |
| Cloud Storage         | Azure Blob Storage                       |
| Image Processing      | OpenCV, Haar Cascade                     |
| Backend Logic         | Python, Kafka Client                     |
| Remote Infrastructure | AWS EC2 Linux VM (for police simulation) |

## System Pipeline

### Step 1: Face Capture and Prediction

* Webcam is activated using OpenCV.
* Haar cascade is used to detect faces from the live stream.
* Detected face images are passed through two CNN models:

  * Gender classification model (Male / Female).
  * Goatee classification model (for Male images only).

### Step 2: Embedding and Cloud Storage

* For every detected face, DeepFace generates a 128-dimensional face embedding.
* The following data is stored in lightweight CSV files and uploaded to Azure Blob Storage:

  * Image ID
  * Gender prediction
  * Goatee prediction
  * Corresponding embedding vector

### Step 3: Suspicion Detection and Co-Presence Analysis

* Given a suspect image, the system retrieves visually similar faces from the stored embeddings.
* It then constructs a list of individuals who were detected at the same time and place, representing them as a friendship tree (graph structure).
* This enables efficient co-occurrence analysis and tracking.

### Step 4: Real-Time Kafka Streaming

* Constructed tree and suspect data are published as Kafka messages using a Python Kafka Producer.
* A Kafka Consumer running on an AWS EC2 instance simulates the law enforcement infrastructure.
* The consumer runs continuously and fetches the tree data in real time for further investigation or visualization.

## How to Run the System

1. Run the face capture and CNN classification system:

   ```bash
   python app.py
   ```
2. Send the suspect tree via Kafka Producer:

   ```bash
   python kafka_producer.py
   ```
3. On AWS or another remote server, run the Kafka Consumer to receive tree data:

   ```bash
   python kafka_consumer.py
   ```

## Folder Structure

```
project-root/
│
├── app.py                        # Real-time camera input and face classification
├── gender_model.h5              # Pretrained gender classification model
├── goatee_model.h5              # Pretrained goatee detection model
├── kafka_producer.py            # Produces messages to Kafka
├── kafka_consumer.py            # Consumes messages from Kafka (runs on AWS)
├── cloud_utils.py               # Azure Blob storage upload/download functions
├── friendship_tree.py           # Constructs co-occurrence trees from data
├── final_merged_code_trial2.ipynb  # Complete notebook containing all workflows
├── embeddings/                  # CSV files containing DeepFace-generated vectors
```

## Use Case: Suspect Identification in Public Spaces

This system provides functionalities to:

* Identify a suspect from an input image by matching with previously stored embeddings.
* Generate a list of individuals who entered the same location during the same time window.
* Construct and send a suspect’s friendship tree to law enforcement in real time.
* Enable security authorities to act quickly using a continuously running cloud-based consumer.

## Future Enhancements

* Integration with high-resolution surveillance camera feeds.
* Cross-camera identity matching using more advanced embedding models.
* Facial attribute expansion: age, emotion, mask detection.
* Improved privacy and audit controls for sensitive biometric data.

## Contributors

This project was developed by:

* Umut Yılmaz
* Fuad Saffedoğlu
* Emre Şahin Demirbaş

Department of Computer Engineering
Çankaya University
