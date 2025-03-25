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
> 
sh train.sh
#predict
cd segment
## Edit your predict.sh
> 
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
    <td><img src="https://user-images.githubusercontent.com/62513924/190402435-931f0ee3-9af1-4399-8222-1028d5afbd1a.png" width=640 height=180></td>
    <td><img src="https://user-images.githubusercontent.com/62513924/190402752-521b7815-bea8-4cef-8b36-54fb7a962244.png" width=640 height=180></td>
    <td><img src="https://user-images.githubusercontent.com/62513924/191729411-a8d8b5e2-bdbf-4c0e-bd1b-a52e23f7c9d3.png" width=640 height=180></td>
  </tr>
  </tr>
 </table>



### References
- [https://github.com/WongKinYiu/yolov7/tree/u7/seg](https://github.com/RizwanMunawar/yolov7-segmentation.git)

