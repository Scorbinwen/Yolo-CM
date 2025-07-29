# YOLOv7-CM: Instance Segmentation

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.12%2B-orange)](https://pytorch.org/)

Official implementation of YOLOv7-CM for instance segmentation, accompanying our paper *[YOLO-CM: Class-Aware Instance Segmentation Using Combine-Mask for Enhanced Object Detection]([(https://link.springer.com/chapter/10.1007/978-981-96-9891-2_35)])*. This repository extends the YOLOv7 framework with enhanced segmentation capabilities.

## 📌 Features
- 🚀 High-performance instance segmentation
- 🧩 Combine-Mask architecture for improved mask prediction
- ⚡ Multi-GPU training support
- 🎯 Results on COCO dataset

## 📦 Installation

### Prerequisites
- Python 3.10.13+
- CUDA 11.8+
- PyTorch 2.1.2+

### Step-by-Step Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/Scorbinwen/Yolo-CM.git
   cd yolov7-segmentation
   ```

2. Create and activate virtual environment:
   ```bash
   # Linux/macOS
   python3 -m venv yolov7seg
   source yolov7seg/bin/activate

   # Windows
   python3 -m venv yolov7seg
   cd yolov7seg/Scripts
   activate
   cd..
   ```

3. Install dependencies:
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

## 🏋️ Training

1. Configure training:
   ```bash
   cd segment
   # Edit train.sh with your parameters
   ```

2. Start training (multi-GPU example):
   ```bash
   sh train.sh
   ```
   *Default command:*
   ```bash
   python -m torch.distributed.launch --nproc_per_node 2 --master_port 29501 --use_env train.py \
       --sync-bn \
       --batch-size 60 \
       --workers 64 \
       --imgsz 640 \
       --device 0,1 \
       --save-period 30 \
       --data../data/coco.yaml \
       --cfg../models/segment/yolov7-seg-combine-mask.yaml \
       --hyp hyp.scratch-high.yaml \
       --combine_mask
   ```

## 🔍 Inference

1. Run prediction:
   ```bash
   cd segment
   # Edit predict.sh with your parameters
   sh predict.sh
   ```
   *Default command:*
   ```bash
   python predict.py \
       --data../data/coco.yaml \
       --weights../weights/best.pt \
       --source /path/to/data
   ```

2. Outputs are saved in:
   ```
   runs/predict-seg/exp/
   ```

## 📊 Results
### 📈 Quantitative Results (COCO test2017)

| Model          | Test Size | APbox  | AP50box | AP75box | APmask | AP50mask | AP75mask | Latency (T4) |
|----------------|-----------|--------|---------|---------|--------|----------|----------|--------------|
| YOLOv7-seg     | 640       | 51.4%  | 69.4%   | 55.8%   | 41.5%  | 65.5%    | 43.7%    | 12.3ms       |
| YOLOv7-CM | 640       | **51.6%** | **70.3%** | **56.2%** | **41.6%** | **65.9%** | **43.9%** | **11.8ms** |

*Table 1: Comparative evaluation on COCO dataset. All metrics reported at IoU threshold 0.50:0.95.*

Key observations:
- ↑ 0.2% improvement in bounding box AP (51.6% vs 51.4%)
- ↑ 0.1% improvement in mask AP (41.6% vs 41.5%)
- ↓ 4% reduction in inference latency

### 🖼️ Visual Results

<div align="center">
  
**Figure 1: Qualitative Segmentation Examples**  
*Left: Original Images - Right: YOLOv7-CM Predictions*

| Methods         | Detection Neatness | Edge Precision | Object Confidence | Detection Integrity |
|-----------------|---------------------|----------------|-------------------|-------------------|
| YOLOv7-seg      | <img src="https://github.com/user-attachments/assets/20d358f2-2722-4849-824b-15bbadf6ec85" width="90%"> | <img src="https://github.com/user-attachments/assets/aa57fdc4-455c-4b3e-82c9-b0c62f4d6647" width="90%"> | <img src="https://github.com/user-attachments/assets/c0748322-2b90-40c3-af9c-dadd2ab48cce" width="90%"> | <img src="https://github.com/user-attachments/assets/424b499d-ac09-40d0-9a88-1e9ca7a34bda" width="90%"> |
| YOLOv7-CM  | <img src="https://github.com/user-attachments/assets/8722d813-c78e-44c7-a6ff-b71df4d856df" width="90%"> | <img src="https://github.com/user-attachments/assets/a90d931b-4fe6-4f16-908d-f7bfc36c70df" width="90%"> | <img src="https://github.com/user-attachments/assets/5f2c69a8-e29a-4471-a732-d9b6fc0dfd06" width="90%"> | <img src="https://github.com/user-attachments/assets/d1696ec5-7c83-44f1-bba8-006f3dc63cb3" width="90%"> |



</div>

## 📜 Citation
```bibtex
@article{wu2025yolocm,
  title={YOLO-CM: Class-Aware Instance Segmentation Using Combine-Mask for Enhanced Object Detection},
  author={Renzhong Wu and Xiaobin Wen and Shenghui Liao and Jianfeng Li and Xiaoyan Kui},
  journal={Springer International Publishing},
  year={2025}
}
```

## 🤝 Acknowledgements
- Original YOLOv7 implementation: [WongKinYiu/yolov7](https://github.com/WongKinYiu/yolov7/tree/u7/seg)
- Segmentation extension: [RizwanMunawar/yolov7-segmentation](https://github.com/RizwanMunawar/yolov7-segmentation)

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
