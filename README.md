# AER850 Project 3 – PCB Object Masking & Component Detection (YOLOv11)

This repository contains all code, figures, and documentation for **AER850 – Project 3**, which focuses on automating PCB inspection using a combination of **OpenCV-based object masking** and **YOLOv11 deep-learning component detection**.  
The project follows a full computer-vision pipeline:

1. Masking and extracting the PCB from the background  
2. Training a YOLOv11-nano model to detect 13 electronic component classes  
3. Evaluating the model on three unseen PCB images (Arduino Uno, Arduino Mega, Raspberry Pi)

This repository includes the Google Colab code, final results, and the report submitted for evaluation.



---

## Project Overview

### Step 1 – PCB Object Masking (OpenCV)

The first part of the project uses classical image-processing techniques to isolate the PCB from the background:

- Grayscale conversion  
- Gaussian blur  
- Otsu thresholding  
- Canny edge detection  
- Largest-contour extraction  
- Mask creation and bitwise extraction  
- Cropping to the final PCB region of interest  

These steps produce a clean, standardized PCB image for training and evaluation.

---

### Step 2 – YOLOv11 Model Training

A YOLOv11-nano model (pretrained on COCO) was fine-tuned on a custom PCB dataset that includes **13 component classes**, such as:

- Resistor  
- Capacitor  
- Diode  
- IC  
- Transistor  
- Pads  
- Pins  
- Connector  
- LED  
- Inductor  
- Button  
- Switch  
- Electrolytic Capacitor  

Training configuration:

- `epochs = 60`  
- `batch = 8`  
- `imgsz = 960`  
- `optimizer = AdamW`  
- `device = T4 GPU (Google Colab)`  
- AMP (Automatic Mixed Precision) enabled  

Generated plots include:

- Normalized confusion matrix  
- Precision–Recall (PR) curves  
- Precision–Confidence curves  
- Training loss curves  

---

### Step 3 – Evaluation on External Images

The final model was tested on three unseen PCB images:

- Arduino Uno  
- Arduino Mega  
- Raspberry Pi  

Evaluations show:

- Strong detection of large components (ICs, connectors, electrolytic capacitors)  
- Moderate detection of medium components (LEDs, pins, switches)  
- Weaker detection of very small or dense components (resistors, pads, diodes)  

This reflects common small-object detection challenges in PCB inspection tasks.

---

## How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name> 
```
2. Install dependencies

Most work was done in Google Colab, but locally you may use:

pip install ultralytics opencv-python matplotlib pillow numpy

3. Run the notebook

Open:

notebooks/project3.ipynb


and follow all numbered steps:

Step 1: Masking and extraction

Step 2: YOLOv11 training

Step 3: Evaluation

4. Inspect results

Annotated images, evaluation plots, and trained weights are stored in:

training/
evaluation/
masking/

Results Summary

Successful PCB masking using OpenCV

YOLOv11-nano achieved approximately mAP50 ≈ 0.60

Strong detection of ICs, connectors, electrolytic capacitors

Small-object classes (resistors, pads, diodes) remain challenging

Model generalizes reasonably to unseen boards (Arduino and Raspberry Pi)

Future Improvements

Train for more epochs (e.g., 100–150)

Use a larger model (YOLOv11-S or YOLOv11-M)

Increase image size to 1280

Balance the dataset or oversample rare classes

Add stronger data augmentation (lighting, rotation, shadows, domain shifts)

References

AER850 Course Team, “Project 3 – PCB Component Detection Assignment,” Toronto Metropolitan University, 2025.

Ultralytics YOLO Documentation – https://docs.ultralytics.com

OpenCV Python Documentation – https://docs.opencv.org

Pillow (PIL) Documentation – https://pillow.readthedocs.io

NumPy Documentation – https://numpy.org/doc

Matplotlib Documentation – https://matplotlib.org

Author

Babak Tafreshi
Aerospace Engineering, Toronto Metropolitan University
AER850 – Winter 2025

::contentReference[oaicite:0]{index=0}







