# Train Rail Fault Detector

A collection of notebooks for training, preprocessing, and deploying YOLO object-detection models on visual inspection tasks, plus a Faster R-CNN benchmark.

## What it does

This repository provides a notebook-based object-detection pipeline:

- Convert image annotations from CSV format to YOLO text labels.
- Train a YOLO model with mosaic, mixup, rotation, scaling, and HSV augmentation.
- Run inference on new images and produce a submission CSV.
- Benchmark a Faster R-CNN (ResNet-50 FPN) model against the YOLO run.

The current notebooks are configured with a crop-disease detection example. The same pipeline can be retargeted to rail-track or other infrastructure inspection by replacing the dataset and the class names in `data.yaml`.

## How it works

- **Data preparation:** `Train.csv` is split into train and validation sets, and bounding boxes are normalized to YOLO format.
- **Preprocessing:** `Preprocessing_Enhancement_Module.ipynb` sets up image and label directories and applies basic brightness enhancement.
- **Training:** `Train_Rail_Fault_Detector.ipynb` trains a YOLO model using Ultralytics, with mixed precision and SGD optimization.
- **Inference:** `Inference_Deploy.ipynb` loads the trained model and writes predicted boxes and classes to `submission.csv`.
- **Benchmark:** `Research_Experiment_FasterRCNN.ipynb` trains a Faster R-CNN detector on the same splits for comparison.

## Tech stack

- Python 3
- Ultralytics YOLO
- PyTorch / torchvision
- OpenCV
- pandas, scikit-learn
- Google Colab or Jupyter

## Results / Metrics

No final evaluation score is committed to the README. The training notebook prints validation metrics such as mAP@50, precision, and recall after each run, so results can be read directly from the notebook outputs. Scores will vary with the dataset and hyperparameters.

## How to run

1. Install dependencies:
   ```bash
   pip install ultralytics opencv-python pandas numpy scikit-learn
   ```
2. Prepare your dataset and update the file paths in the notebooks.
3. Run `Preprocessing_Enhancement_Module.ipynb` to build the YOLO directory structure.
4. Run `Train_Rail_Fault_Detector.ipynb` to train the YOLO model.
5. Run `Inference_Deploy.ipynb` to generate predictions on new images.
6. (Optional) Run `Research_Experiment_FasterRCNN.ipynb` to compare with Faster R-CNN.

## Project status

Notebook pipeline template; currently configured with a crop-disease example, retargetable to rail inspection or other visual-inspection tasks by replacing the dataset and `data.yaml` class names.

## License

No license is specified in this repository.

---

## Suggested GitHub metadata

**Suggested descriptions (<=160 chars):**

1. YOLO object-detection training, inference, and Faster R-CNN benchmarking notebooks for visual inspection.
2. Notebook-based YOLO pipeline for visual inspection, with a Faster R-CNN benchmark.

**Suggested topic tags:**

`yolo`, `object-detection`, `ultralytics`, `pytorch`, `computer-vision`
