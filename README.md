# yolov7-Harmony-instance-segmentation


## Steps to run Code

- Clone the repository
```bash
git clone https://github.com/Scorbinwen/Yolo-Harmony.git
```
- Goto the cloned folder.
```bash
cd yolov7-segmentation
```
- Create a virtual envirnoment (Recommended, If you dont want to disturb python packages)
```bash
### For Linux Users
python3 -m venv yolov7seg
source yolov7seg/bin/activate

### For Window Users
python3 -m venv yolov7seg
cd yolov7seg
cd Scripts
activate
cd ..
```
- Upgrade pip with mentioned command below.
```bash
pip install --upgrade pip
```
- Install requirements with mentioned command below.
```bash
pip install -r requirements.txt
```
- Download weights from [link](https://github.com/RizwanMunawar/yolov7-segmentation/releases/download/yolov7-segmentation/yolov7-seg.pt)and store in "yolov7-segmentation" directory, note that this weight is just the yolov7 baseline model,
  the Yolo-Harmony model will be released in a few weeks.

- Run the code with mentioned command below.
```bash
#train
cd segment
## Edit your train.sh
> python -m torch.distributed.launch --nproc_per_node 2  --master_port 29501 --use_env train.py --sync-bn --batch-size 60 --workers 64 --imgsz 640 --device 0,1 --save-period 30 --data ../data/coco.yaml --cfg ../models/segment/yolov7-seg-combine-mask.yaml  --hyp hyp.scratch-high.yaml --combine_mask
sh train.sh
#predict
cd segment
## Edit your predict.sh
> python predict.py  --data ../data/coco.yaml  --weights ../weights/best.pt --source /path/to/data
sh predict.sh
```

- Output file will be created in the working directory with name <b>yolov7-segmentation/runs/predict-seg/exp/"original-video-name.mp4"</b>

### RESULTS
<table>
  <tr>
    <td>Car Semantic Segmentation</td>
     <td>Car Semantic Segmentation</td>
     <td>Person Segmentation + Tracking</td>
     </tr>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/8722d813-c78e-44c7-a6ff-b71df4d856df"></td>
    <td><img src="https://github.com/user-attachments/assets/d1696ec5-7c83-44f1-bba8-006f3dc63cb3"></td>
    <td><img src="https://github.com/user-attachments/assets/df5297f5-71ca-4e56-b95f-41543b798c17"></td>
  </tr>
  </tr>
 </table>



### References
- [https://github.com/WongKinYiu/yolov7/tree/u7/seg](https://github.com/RizwanMunawar/yolov7-segmentation.git)

