# 🛡️ SafeSite AI – PPE Detection & Compliance System

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python)
![YOLOv8](https://img.shields.io/badge/YOLOv8-blueviolet?style=for-the-badge)
![ONNX](https://img.shields.io/badge/ONNX-Export-green?style=for-the-badge&logo=onnx)
![Patent Status](https://img.shields.io/badge/Patent%20Status-Pending-blue?style=for-the-badge)

SafeSite AI is an advanced computer vision system designed to enhance workplace safety on construction and industrial sites. It goes beyond simple object detection by not only identifying the **presence** of six critical Personal Protective Equipment (PPE) items but also verifying their **correct placement** on individuals.

This multi-stage validation process, combining state-of-the-art detection with custom rule-based logic, significantly reduces false positives and provides a more accurate and reliable automated compliance monitoring solution.

---

## 📸 System in Action

This section showcases the output of the SafeSite AI system, from raw detections to final compliance reports.

| Multi-Class PPE Detection |
| :-----------------------: |
| *[Add an image here showing YOLOv8 detecting multiple PPE items like helmets, vests, and masks in a single frame]* |
| **(Placeholder for Detection Image)** |

| Pose Verification (Helmet Check) |
| :------------------------------: |
| *[Add an image here demonstrating a "non-compliant" flag for a worker holding a helmet instead of wearing it]* |
| **(Placeholder for Pose-Check Image)** |

| Instance Segmentation in Crowded Scenes | Compliance Log Output |
| :-------------------------------------: | :-------------------: |
| *[Add an image here showing R-CNN correctly assigning PPE to multiple workers who are close together or overlapping]* | *[Add an image or code block here showing an example of the audit log (e.g., Image ID + Timestamp + Violation)]* |
| **(Placeholder for Segmentation Image)** | **(Placeholder for Log Image)** |

---

## 📋 Table of Contents

- [The Problem It Solves](#-the-problem-it-solves)
- [System Architecture & Workflow](#️-system-architecture--workflow)
- [Performance Metrics](#-performance-metrics)
- [Dataset and Model](#-dataset-and-model)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)

---

## 🎯 The Problem It Solves

SafeSite AI addresses critical gaps left by traditional PPE detection systems:

1.  **Lack of Pose-Based Verification**: Most systems detect a PPE item's presence but can't tell if it's being worn correctly. A helmet on the ground is not protecting a worker.
    -   **Our Solution**: We implement a positional rule engine, such as verifying a helmet's bounding box is correctly positioned above a person's head, to validate proper use and minimize false positives.

2.  **Poor Performance in Crowded Scenes**: In images with multiple workers, simple bounding boxes can fail to assign the correct PPE to the right person, leading to inaccurate compliance data.
    -   **Our Solution**: By using **R-CNN for instance segmentation**, our system can isolate individual PPE items even when they overlap, ensuring each piece of equipment is correctly attributed to the right person.

3.  **Limited PPE Coverage**: Many solutions focus only on helmets, ignoring other critical safety gear.
    -   **Our Solution**: Our model is trained to detect a comprehensive set of **six PPE classes**: helmets, gloves, boots, vests, glasses, and masks, providing a holistic view of site safety.

---

## ⚙️ System Architecture & Workflow

The system processes images through a multi-stage pipeline to ensure accurate compliance assessment:

1.  **Image Ingestion**: The system takes static images as input, either from offline datasets or batch uploads for analysis.
2.  **Multi-Class Detection (YOLOv8)**: The powerful **YOLOv8** model performs the initial scan, identifying all six classes of PPE and generating bounding boxes.
3.  **Instance Segmentation (R-CNN)**: In complex scenes, an **R-CNN** model is used to create pixel-level masks for each detected item, enabling precise association with individuals.
4.  **Pose-Based Verification**: A custom logic layer checks the geometric relationship between a person and their PPE (e.g., is the helmet above the head?).
5.  **Compliance Evaluation Engine**: The final engine aggregates all data to make a compliance decision (Compliant / Non-Compliant) and generates an auditable log with an image ID and timestamp for each violation.

---

## 🛠️ Core Technologies

-   **Object Detection**: **YOLOv8**, trained for 50 epochs on a dataset of over 3,800 labeled images.
-   **Instance Segmentation**: **R-CNN** for handling occlusions and crowded environments.
-   **Deployment**: The final model is exported to **ONNX** format, making it highly portable and ready for deployment in various production environments.
-   **Logic Engine**: A custom rule-based engine for pose verification and compliance evaluation.

---

## 📊 Performance Metrics

The model demonstrates strong performance in both detection and classification, validated by the following metrics:

| Metric | Score | Description |
| :--- | :---: | :--- |
| **Precision** | 0.90 | 90% of the model's detections were correct, minimizing false alarms. |
| **Recall** | 0.85 | The model successfully identified 85% of all true PPE instances in the images. |
| **mAP@.50** | 0.95 | Excellent performance in detecting objects with a relaxed overlap threshold. |
| **mAP@.50-.95**| 0.70 | A stricter metric indicating solid performance, with room for improvement in precise localization. |

Training was successful, with all loss components (Box, Classification, DFL) showing consistent decreases on both training and validation sets, indicating robust learning.

---

## 💾 Dataset and Model

The resources used and produced by this project are available at the links below.

-   **Dataset**: The training dataset consists of over 3,800 labeled images.
    -   ➡️ **[LINK TO YOUR DATASET HERE]**
-   **Trained Model**: The final trained model is available in ONNX format for easy deployment.
    -   ➡️ **[LINK TO YOUR TRAINED MODEL HERE]**

---

## 🚀 Getting Started

To get a local copy up and running, follow these simple steps.

1.  **Clone the Repository**
    ```sh
    git clone [https://github.com/YOUR_USERNAME/SafeSite-AI.git](https://github.com/YOUR_USERNAME/SafeSite-AI.git)
    cd SafeSite-AI
    ```
2.  **Create and Activate a Virtual Environment**
    ```sh
    python -m venv venv
    source venv/bin/activate
    ```
3.  **Install Dependencies**
    ```sh
    pip install -r requirements.txt
    ```
4.  **Run the System**
    ```sh
    python main.py --image path/to/your/image.jpg
    ```

---

## 📂 Project Structure

```text
.
├── assets/              # Images for README and documentation
├── data/                # Placeholder for training/testing data
├── models/              # Contains the exported ONNX model
├── notebooks/           # Jupyter notebooks for experimentation and analysis
├── src/                 # Source code for the detection and compliance engine
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
