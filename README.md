# Slim Object Direct Offset (SODO):Object Detection

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.12%2B-orange)](https://pytorch.org/)

Official implementation of SODO for Object Detection, accompanying our paper *[Slim Object Direct Offset (SODO): Why YOLO with TOOD struggles to detect slim objects? A new matching approach for slim objects]()*. This repository remedies TOOD for slim object detection.

## 📌 Features
- 🚀 High-performance Object Detection for Slim Objects
- 🧩 SODO Method for slim object target matching.
- ⚡ Multi-GPU training support
- 🎯 Results on COCO dataset & tans & pole_detection on Roboflow dataset.

## 📦 Installation

### Prerequisites
- Python 3.10.13+
- CUDA 11.8+
- PyTorch 2.1.2+

### Step-by-Step Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/Scorbinwen/SODO.git
   cd SODO
   ```

2. Create and activate virtual environment refer to [ultralytics](https://github.com/ultralytics/ultralytics)
   

4. Install dependencies:
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```
   (do not install ultralytics pip package, because our SODO repo has not submit to ultralytics official code hub yet.)
## 🏋️ Training

1. Configure training:
   ```bash
   cd script
   # Edit train.sh with your parameters
   ```

2. Start training (multi-GPU example):
   ```bash
   sh train.sh
   ```
   *example script:*
   ```bash
   # train artificial slim obj regmax sub one + with layer_wise_assign + 20 epochs layer wise assign
   python train.py --model ../ultralytics/cfg/models/11/yolo11l_regmax.yaml \
   --data ../ultralytics/cfg/datasets/artifical_slim_obj.yaml  --device "0,1,2,3,4,5,6,7" \
   --save_period 10 --epochs 200 --batch 400 --reg_max_sub_one True --use_center_offset False \
   --amp False --layer_wise_assign True --slim_obj_assign True --imgsz 320 --close_layer_wise_assign 0.2
   ```

## 🔍 Inference

1. Run prediction:
   ```bash
   cd segment
   # Edit predict.sh with your parameters
   sh predict.sh
   ```
   *example script:*
   ```bash
   python predict.py \
       --data../data/coco.yaml \
       --weights../weights/best.pt \
       --source /path/to/data
       --name your_pred_results
   ```

2. Outputs are saved in:
   ```
   runs/predict-seg/your_pred_results/
   ```

## 📊 Results
### 📈 Quantitative Results (COCO test2017 & pole_detection & tans)

| Model               | COCO val mAP₅₀ | COCO val mAP₅₀-₉₅ | COCOSlim mAP₅₀ | COCOSlim mAP₅₀-₉₅ | pole_detection test mAP₅₀ | pole_detection test mAP₅₀-₉₅ | tans test mAP₅₀ | tans test mAP₅₀-₉₅ |
|---------------------|----------------|-------------------|----------------|-------------------|---------------------------|------------------------------|-----------------|--------------------|
| v11-L               | 0.702          | 0.534             | 0.721          | 0.562             | 0.824                     | 0.569                        | 0.695           | 0.494              |
| v11-L (SODO) **Ours** | **0.705**      | 0.530             | **0.731**      | 0.561             | **0.836**                 | **0.580**                    | **0.712**       | **0.501**          |
| v12-L               | 0.708          | 0.538             | 0.724          | 0.559             | 0.813                     | 0.566                        | 0.705           | 0.489              |
| v12-L (SODO) **Ours** | **0.711**      | 0.537             | **0.731**      | 0.558             | **0.832**                 | **0.578**                    | **0.729**       | **0.499**          |
| v13-L               | 0.709          | 0.581             | 0.740          | 0.577             | 0.816                     | 0.568                        | 0.738           | 0.531              |
| v13-L (SODO) **Ours** | **0.712**      | 0.580             | **0.746**      | 0.577             | **0.825**                 | **0.574**                    | **0.742**       | 0.501              |

*Table 1: Comparative evaluation on COCO test2017 & pole_detection & tans dataset. All metrics reported at IoU threshold 0.50:0.95.*


### 🖼️ Visual Results(Baseline is YOLO11-L)

<div align="center">
  
**Figure 1: Qualitative Slim Object Detection Examples on COCO2017 Dataset**  
<img width="647" height="348" alt="image" src="https://github.com/user-attachments/assets/55b6ff03-dcd8-4d90-ab52-b9973c9a4d3f" />

**Figure 2: Qualitative Slim Object Detection Examples on pole_detection Dataset**  
<img width="647" height="350" alt="image" src="https://github.com/user-attachments/assets/1b29eb97-26e2-42aa-85dc-436d3a856959" />

**Figure 3: Qualitative Slim Object Detection Examples on tans Dataset**  
<img width="647" height="346" alt="image" src="https://github.com/user-attachments/assets/7a011575-f30e-493c-bd52-088e0781ff89" />



</div>

## 📜 Citation
```bibtex
@article{wu2025yolocm,
  title={Slim Object Direct Offset (SODO): Why YOLO with TOOD struggles to detect slim objects? A new matching approach for slim objects},
  author={Renzhong Wu and Xiaobin Wen and Shenghui Liao and Jianfeng Li and Xiaoyan Kui},
  journal={Springer International Publishing},
  year={2025}
}
```

## 🤝 Acknowledgements
- Original ultralytics YOLO implementation: [ultralytics YOLO](https://github.com/ultralytics/ultralytics)
- [pole_detection](https://universe.roboflow.com/poleproject/pole-detection-v2-bvqug) & [tans](https://universe.roboflow.com/2crack500/long-tans) dataset

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
