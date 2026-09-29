# Digital KYC: Identity Verification & Liveness Detection in Kenya 🇰🇪

## Project Overview

As financial services in Kenya become increasingly digital, there is a growing need for secure ways of verifying customer identities remotely.

This project aims to develop a **Digital Know Your Customer (KYC) prototype** using computer vision and deep learning. The system will compare the photograph on an identification document with a user's selfie and perform a liveness check to determine whether a real person is present.

## Problem Statement

Digital customer onboarding can be vulnerable to identity fraud. A person may attempt to register using another person's identification document or present a printed photograph to the camera during verification.

Face matching alone may confirm that a face matches the ID without determining whether the actual person is physically present.

This project therefore combines **face detection, face verification, and liveness detection** to support a more secure digital identity verification process.

## Objectives

- Detect and crop faces from ID documents and selfies using YOLO.
- Compare the ID photograph with the user's selfie.
- Determine whether the two faces belong to the same person.
- Detect whether a real person or printed photograph is presented to the camera.
- Extract basic information from the ID using OCR.
- Generate a final identity verification result.
- Deploy the system using FastAPI.

## Datasets

### 1. Face Verification Dataset

The project will use the **Axon Selfie and Official ID Photo Dataset** from Kaggle.

The dataset contains ID photographs and multiple selfies belonging to different individuals.

It will be used to train the face verification model to determine:

- **Match** – ID photograph and selfie belong to the same person.
- **No Match** – ID photograph and selfie belong to different people.

### 2. Liveness Detection Dataset

Axon anti-spoofing datasets will be used for liveness detection:

- **Real Dataset** – represents real people (**Live**).
- **Photo Print Attack Dataset** – represents printed photographs presented to a camera (**Spoof**).

The model will learn to classify an input as:

```text
LIVE  → Real person
SPOOF → Printed photograph
```

### 3. Mock Kenyan IDs

Mock Kenyan IDs will be created using **Canva** for final testing and demonstration.

The mock IDs will contain fictional information and will not be used to train the models.

## Proposed Workflow

```text
             ID Image + Selfie
                    │
                    ▼
            YOLO Face Detection
              & Face Cropping
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
   Face Verification     Liveness Detection
    Match / No Match       Live / Spoof
          │                   │
          └─────────┬─────────┘
                    ▼
              OCR Extraction
                    │
                    ▼
           Verification Result
                    │
                    ▼
                 FastAPI
```

## Models

### YOLO – Face Detection

A pretrained **YOLO face detector** will be used to locate and crop faces from the ID document and selfie before they are passed to the other models.

### Siamese Neural Network – Face Verification

A **Siamese Neural Network** will be used to compare the face extracted from the ID with the user's selfie and determine whether they belong to the same person.

### CNN – Liveness Detection

A **CNN-based model** will be trained to distinguish between:

- **Live** – a real person is present.
- **Spoof** – a printed photograph is presented to the camera.

## Verification Decision

A successful verification will require:

```text
Face Match = YES
       +
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

## Tools

- Python
- PyTorch
- YOLO
- OpenCV
- Siamese Neural Network
- CNN
- OCR
- FastAPI
- Canva

## Expected Outcome

The final system will accept an identification document and a selfie and provide a result such as:

```text
Face Detected: Yes
Face Match: Yes
Liveness: Live
Status: Verified
```

The project will demonstrate how **computer vision and deep learning can support Digital KYC and identity verification in the Kenyan financial sector**.
