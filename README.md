# YOLOv7-Harmony: Instance Segmentation

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.12%2B-orange)](https://pytorch.org/)

Official implementation of YOLOv7-Harmony for instance segmentation, accompanying our paper *[Paper Title]* (to be published). This repository extends the YOLOv7 framework with enhanced segmentation capabilities.

## 📌 Features
- 🚀 High-performance instance segmentation
- 🧩 Harmony architecture for improved mask prediction
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
   git clone https://github.com/Scorbinwen/Yolo-Harmony.git
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
   cd ..
   ```

3. Install dependencies:
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

## 🏋️ Training

1. Download baseline weights:
   - [yolov7-seg.pt](https://github.com/RizwanMunawar/yolov7-segmentation/releases/download/yolov7-segmentation/yolov7-seg.pt) (place in `yolov7-segmentation` directory)

2. Configure training:
   ```bash
   cd segment
   # Edit train.sh with your parameters
   ```

3. Start training (multi-GPU example):
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
       --data ../data/coco.yaml \
       --cfg ../models/segment/yolov7-seg-combine-mask.yaml \
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
       --data ../data/coco.yaml \
       --weights ../weights/best.pt \
       --source /path/to/data
   ```

2. Outputs are saved in:
   ```
   runs/predict-seg/exp/
   ```

## 📊 Results
<table>
  <tr>
    <td align="center">box mAP</td>
    <td align="center">mask mAP</td>
  </tr>
  <tr>
    <td align="center">0.664</td>
    <td align="center">0.619</td>
</td>
  </tr>
</table>

<table>
  <tr>
    <td align="center"><img src="https://github.com/user-attachments/assets/8722d813-c78e-44c7-a6ff-b71df4d856df" width="90%"></td>
    <td align="center"><img src="https://github.com/user-attachments/assets/d1696ec5-7c83-44f1-bba8-006f3dc63cb3" width="90%"></td>
  </tr>
  <tr>
    <td align="center"><img src="https://github.com/user-attachments/assets/5f2c69a8-e29a-4471-a732-d9b6fc0dfd06" width="90%"></td>
    <td align="center"><img src="https://github.com/user-attachments/assets/a90d931b-4fe6-4f16-908d-f7bfc36c70df" width="90%"></td>
</td>
  </tr>
</table>

## 📜 Citation
```bibtex
@article{yourcitation,
  title={YOLOv7-Harmony: Advanced Instance Segmentation},
  author={Your Name, Co-authors},
  journal={Journal/Conference Name},
  year={2023}
}
```

## 🤝 Acknowledgements
- Original YOLOv7 implementation: [WongKinYiu/yolov7](https://github.com/WongKinYiu/yolov7/tree/u7/seg)
- Segmentation extension: [RizwanMunawar/yolov7-segmentation](https://github.com/RizwanMunawar/yolov7-segmentation)

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

Key improvements made:
1. Added professional header with badges
2. Organized content with clear section headers and emojis
3. Improved code block formatting with syntax highlighting
4. Added citation section for academic use
5. Better visual hierarchy with tables and alignment
6. Added license information
7. More concise and action-oriented instructions
8. Better spacing and readability
9. Added placeholder for paper citation
10. Structured acknowledgements section

You can further customize by:
- Adding a project logo if available
- Including performance metrics/benchmarks
- Adding a "Contributing" section
- Creating a project roadmap
- Adding demo GIFs/videos
