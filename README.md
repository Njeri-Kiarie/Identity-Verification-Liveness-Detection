# Digital KYC: Identity Verification & Liveness Detection in Kenya 🇰🇪

## Project Overview

As financial services in Kenya become increasingly digital, there is a growing need for secure ways of verifying customer identities remotely.

This project aims to develop a **Digital KYC prototype** using computer vision and deep learning. The system will compare the face on an identification document with a customer's selfie and perform liveness detection to determine whether a real person is present.

The system is designed as an identity-verification component that could be integrated into existing digital onboarding platforms used by banks, FinTech companies, digital lenders, SACCOs and other financial service providers.

## Problem Statement

Remote customer onboarding can be vulnerable to identity fraud. For example, a person may attempt to register using another person's identification document or present a photograph instead of being physically present.

Face matching alone may determine whether two facial images belong to the same person, but it does not confirm that a real person is present during verification.

This project therefore combines **face detection, face verification and liveness detection** to provide a more complete identity-verification process.

## Objectives

- Detect and crop faces from ID documents and selfies using YOLO.
- Compare the ID photograph with the customer's selfie.
- Determine whether the two faces belong to the same person.
- Detect whether the selfie represents a live person or a spoof attempt.
- Extract basic information from the ID using OCR.
- Generate a final KYC verification result.
- Deploy the verification pipeline using FastAPI.

## Datasets

### 1. Face Verification Dataset

The project will use the **Axon Selfie and Official ID Photo public dataset**.

The available sample contains:

- 10 different identities.
- ID document photographs.
- Current selfies captured under different conditions.
- Archive selfies.

Because the available dataset is small, it will **not be used to train a face-recognition model from scratch**. Instead, it will be used to create genuine and impostor face pairs for testing the face-verification pipeline.

The verification classes will be:

- **1 – Match:** ID photograph and selfie belong to the same person.
- **0 – No Match:** ID photograph and selfie belong to different people.

### 2. Liveness Detection Dataset

The liveness component will use separate images representing:

- **Live:** A real person captured by a camera.
- **Spoof:** A printed photograph presented to the camera.

These images will be used to train a binary image-classification model for liveness detection.

### 3. Mock Kenyan IDs

Fictional Kenyan-style identification documents will be created for the final demonstration.

These IDs will contain fictional information and will be clearly marked as samples. They will only be used for testing and demonstrating the completed system.

## Proposed Workflow

```text
ID Image                         Selfie
    ↓                              ↓
YOLO Face Detection          YOLO Face Detection
    ↓                              ↓
ID Face                         Selfie Face
      \                           /
       \                         /
              ArcFace
                 ↓
          Face Embeddings
                 ↓
          Cosine Similarity
                 ↓
          Match / No Match


Selfie
   ↓
Liveness Detection CNN
   ↓
Live / Spoof


ID Image
   ↓
OCR
   ↓
Extract ID Information


Face Verification + Liveness
              ↓
       Final KYC Decision
              ↓
    Verified / Not Verified
```

## Models

### YOLO Face Detection

A pretrained YOLO face-detection model will be used to locate and crop faces from ID photographs and selfies before face verification.

### ArcFace Face Verification

A pretrained **ArcFace** model will generate numerical face embeddings for the ID photograph and selfie.

The embeddings will be compared using similarity measurement to determine whether the two images belong to the same person.

The output will be:

- **Match**
- **No Match**

### Liveness Detection CNN

A Convolutional Neural Network (CNN) will be trained to distinguish between:

- **Live**
- **Spoof**

This helps prevent someone from passing verification simply by presenting a printed photograph of the correct person.

### OCR

Optical Character Recognition (OCR) will be used to extract basic text information from the identification document.

## Verification Decision

The final verification decision will combine face verification and liveness detection.

```text
Face Match = YES
Liveness = LIVE
        ↓
     VERIFIED
```

If the face does not match or a spoof is detected:

```text
Face Match = NO
      OR
Liveness = SPOOF
        ↓
   NOT VERIFIED
```

## Tools and Technologies

- Python
- OpenCV
- YOLO
- ArcFace
- Convolutional Neural Networks (CNN)
- OCR
- FastAPI
- Canva

## Expected Outcome

The completed prototype will accept an ID image and selfie and produce a result similar to:

```text
Face Detected: Yes
Face Match: Yes
Liveness: Live
Status: Verified
```

The project will demonstrate how computer vision and deep learning techniques can be combined to support Digital KYC identity verification in the Kenyan financial sector.
