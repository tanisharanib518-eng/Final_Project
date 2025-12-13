Prosthetic Hippocampal Emulator

EEG-Based Memory Encoding & Recall Classification using Deep Learning (PyTorch) With Assistive Memory App Logic

📌 Overview

This project implements a non-invasive digital hippocampal prosthesis using EEG signals.

It performs:

EEG Preprocessing & Wave Extraction (theta, alpha, beta, gamma)

Image Generation of EEG Segments

CNN-based Classification (Encoding vs Recall)

Memory Logging & Recall App

Context-Aware Retrieval based on time proximity

The system simulates how the brain encodes and recalls memory, providing assistive functionality for patients with memory impairments.

🚀 Project Features

🔹 1. EEG Preprocessing

Loads PhysioNet EEGMMIDB dataset (.edf)

Applies filtering (1–45 Hz)

Extracts band powers (theta, alpha, beta, gamma)

🔹 2. EEG Image Generation

Converts each recording into .png images (per subject & session)

Images stored in:

outputs/SubjectXX_Y.png

🔹 3. CNN Model (PyTorch)

Uses ResNet18 modified for 1-channel EEG images

Trained to classify:

encode

recall

Model saved as:

outputs/memory_cnn.pth

🔹 4. Assistive Memory Application

Uses trained CNN to detect encoding or recall events

On encode → asks user for:

memory text

desired time

logs into memory_db.json

On recall → retrieves memory closest to current system time

Works like a digital hippocampus replacement.

📁 Project Structure

prosthetic_hippocampal_using_cnn/

│
├── eegmmidb/                  # Raw .edf EEG dataset

├── outputs/                   # Generated EEG images + trained model

│   ├── memory_cnn.pth

│   └── SubjectXX_Y.png

│
├── features/
│   └── eeg_band_features.csv  # Extracted band powers & dominant wave

│
├── cnn_dataset/               # Auto-generated CNN training dataset

│   ├── encode/

│   └── recall/

│
├── app_logic/

│   └── memory_app.py          # Main user-facing memory assistant
│
├── src/

│   ├── load_and_preprocess_eeg.py

│   ├── feature_extraction.py

│   ├── prepare_cnn_dataset.py

│   └── train_pytorch_cnn.py
│
└── README.md

⚙️ Installation

1. Create Virtual Environment
   
python -m venv cnn_env

cnn_env\Scripts\activate   # Windows

3. Install Dependencies
   
pip install torch torchvision torchaudio

pip install mne numpy pandas matplotlib pillow

🧩 Step-by-Step Usage

STEP 1 — Preprocess EEG & Generate Images

python src/load_and_preprocess_eeg.py


Outputs go into: outputs/SubjectXX_Y.png

STEP 2 — Extract EEG Band Features

python src/feature_extraction.py


Saves:

features/eeg_band_features.csv

STEP 3 — Prepare CNN Dataset Based on Dominant Wave

python src/prepare_cnn_dataset.py


Auto-classifies encoding vs recall using band dominance.

STEP 4 — Train CNN Model

python src/train_pytorch_cnn.py


Model saved to:

outputs/memory_cnn.pth

STEP 5 — Run Memory Assistant

python app_logic/memory_app.py


Example Interaction:

Enter EEG image path:

> test_samples/test1.png

🧠 Classified as: ENCODE

What should I remember?

> Buy milk

At what time? (HH:MM)

> 17:00

Saved to memory_db.json


On recall:

🧠 Classified as: RECALL

Closest memory to current time:

Buy milk at 17:00

🧪 Model Details

Architecture: Modified ResNet18

Input: 1-channel grayscale EEG image (224 × 224)

Output classes: encode, recall

Optimizer: Adam

Loss: CrossEntropy

Accuracy: Depends on dataset wave separation

🎯 Objective of the Project

Build a non-invasive hippocampal prosthesis emulator

Detect memory encoding/recall patterns using EEG

Provide AI-assisted memory logging

Retrieve memories based on time-context, imitating natural recall

📚 Dataset

Uses PhysioNet EEG Motor Movement/Imagery Dataset (EEGMMIDB).

Download Link:
https://physionet.org/content/eegmmidb/1.0.0/

🤝 Contributing

Pull requests are welcome!
