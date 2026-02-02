# RailTrack AI: Autonomous Fault Detection System

### 1. The "So What?" (Project Mandate)
Manual inspection of thousands of kilometers of rail track is slow, error-prone, and dangerous. This project implements an **Autonomous Defect Detection System** capable of identifying critical structural failures (e.g., broken rails, missing fasteners) from high-velocity drone or rolling-stock imagery.

**Core Objective:** Minimize derailment risk by reducing the "Detection-to-Action" latency, automating the classification of track anomalies with >0.7 mAP (Mean Average Precision).

### 2. Methodological Rigor
* **High-Resolution Tiling:** Standard resizing destroys small defect details (e.g., hairline cracks). This pipeline utilizes a **Sliding Window / Tiling** approach (1200p input) to preserve pixel density for small object detection.
* **Architecture:** Deployed **YOLOv11s** (You Only Look Once), optimized for the edge-compute constraints of inspection drones (Trade-off: Speed vs. Accuracy).
* **Augmentation Strategy:** Implemented aggressive domain randomization (Mosaic, MixUp) to handle varying lighting conditions (dawn/dusk inspections) and track textures.
### 2.1 Model Selection & Preprocessing
* **Architectural Tournament:** We benchmarked **Faster R-CNN (ResNet50 backbone)** against **YOLOv11**. While R-CNN offered slightly higher recall on small defects, YOLOv11 was selected for production due to a 400% increase in inference speed (FPS) suitable for drone deployment.
* **Signal Enhancement:** Raw footage often suffers from motion blur and low contrast. We implemented a **CLAHE (Contrast Limited Adaptive Histogram Equalization)** pipeline (`Preprocessing_Enhancement_Module.ipynb`) to normalize lighting variance before inference.

### 3. Key Metrics
* **mAP@50:** Primary accuracy metric for bounding box precision.
* **Inference Speed:** optimized for near real-time processing.
* **False Positive Rate:** Tuned via confidence thresholding to prevent alarm fatigue in control centers.

### 4. Tech Stack
* **Deep Learning:** PyTorch, Ultralytics YOLOv11.
* **Data Processing:** OpenCV (Image Tiling), Albumentations.
* **Inference:** Pandas (Submission formatting).

### 5. Quick Start
1.  **Install Dependencies:**
    ```bash
    pip install ultralytics opencv-python pandas numpy
    ```
2.  **Training (Research):**
    Run `Train_Rail_Fault_Detector.ipynb` to train the YOLO model on tiled datasets.
3.  **Inference (Production):**
    Run `Inference_Deploy.ipynb` to load `best.pt` and generate `submission.csv` for unseen test data.

### 6. Repository Structure