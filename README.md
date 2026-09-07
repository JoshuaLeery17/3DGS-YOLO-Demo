# 3DGS-YOLO-Demo

> 🧩 A lightweight zero-training demo connecting **pretrained 3D Gaussian Splatting (3DGS)** with **pretrained YOLO object detection**.

This project explores whether RGB views rendered from a pretrained 3D Gaussian scene can be directly used by an off-the-shelf 2D object detector.

No additional 3DGS or YOLO training is performed.

---

## 🔍 Overview

The pipeline is:

```text
Pretrained 3DGS Scene
        ↓
DirectXSplat Rendering
        ↓
Rendered RGB Views
        ↓
Pretrained YOLO
        ↓
2D Object Detection

## 🖥️ Environment

- Windows 10
- NVIDIA GeForce RTX 3060 Laptop GPU (6GB VRAM)
- CUDA 11.8
- PyTorch 2.1.2 + cu118
- NumPy 1.26.4
- Ultralytics 8.4.142
- DirectXSplat

---

## 🖼️ Rendered Views

| View 01 | View 02 | View 03 |
|---|---|---|
| ![](outputs/kitchen_view_01.png) | ![](outputs/kitchen_view_02.png) | ![](outputs/kitchen_view_03.png) |

---

## 🎯 Detection Results

### YOLO11n

| View 01 | View 02 | View 03 |
|---|---|---|
| ![](yolo_results/kitchen_demo-yolo11n/kitchen_view_01.jpg) | ![](yolo_results/kitchen_demo-yolo11n/kitchen_view_02.jpg) | ![](yolo_results/kitchen_demo-yolo11n/kitchen_view_03.jpg) |

### YOLO11m

| View 01 | View 02 | View 03 |
|---|---|---|
| ![](yolo_results/kitchen_retry-yolo11m/kitchen_view_01.jpg) | ![](yolo_results/kitchen_retry-yolo11m/kitchen_view_02.jpg) | ![](yolo_results/kitchen_retry-yolo11m/kitchen_view_03.jpg) |

---

## 📊 YOLO11n vs YOLO11m

| Model | Observation |
|---|---|
| YOLO11n | Lightweight and fast, but misses some objects in difficult rendered views |
| YOLO11m | Detects more objects, but may introduce additional false positives |

The results suggest that detector capacity affects object recognition performance on rendered 3DGS views.

---

## 🚀 How to Run

### 3DGS Rendering

```bat
build\bin\Release\DirectXSplatViewer.exe "models\kitchen\checkpoint\point_cloud\iteration_30000\point_cloud.ply"

yolo predict model=yolo11n.pt source="outputs" imgsz=960 conf=0.25 device=0 save=True

yolo predict model=yolo11m.pt source="outputs" imgsz=1280 conf=0.15 device=0 save=True

🔭 Future Work
UI-free offscreen rendering
Open-vocabulary object detection
2D semantic ROI to 3D Gaussian association
Task-relevant Gaussian selection
Robotic perception and manipulation


## 🙏 Acknowledgements

This project builds upon:

- [DirectXSplat](https://github.com/pbkx/DirectXSplat)
- [3D Gaussian Splatting](https://github.com/graphdeco-inria/gaussian-splatting)
- [Ultralytics YOLO](https://github.com/ultralytics/ultralytics)
