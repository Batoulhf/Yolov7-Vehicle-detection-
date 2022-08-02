# Yolov7-Vehicle-detection-
Real time vehicle detection using yolov7 using colab
[![open in colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Obk_IkJM3rIKW6OUczLvS_qiuB8N8pqQ?authuser=4#scrollTo=0W0MpUaTCJro)

Implementation of paper - [YOLOv7: Trainable bag-of-freebies sets new state-of-the-art for real-time object detectors](https://arxiv.org/abs/2207.02696)

## Install Dependencies
Download YOLOv7 repository and install requirements :

```

!git clone https://github.com/WongKinYiu/yolov7

```
## Download Correctly Formatted Custom Data
Annotate own dataset using [Roboflow annotate](https://roboflow.com/annotate) - a self-serve image annotation tool built right into Roboflow.
Next, we'll download our dataset in the right format. Use the YOLOv7 PyTorch export. Note that this model requires YOLO TXT annotations, a custom YAML file, and organized directories. The roboflow export writes this for us and saves it in the correct spot.

### Training

```
!python train.py --batch 16 --cfg cfg/training/yolov7.yaml --epochs 100 --data {dataset.location}/data.yaml --weights 'yolov7.pt' --device 0

```
### Testing
```
!python test.py --data /data.yaml --img 640 --batch 32 --conf 0.001 --iou 0.65 --device 0 --weights /best.pt --name yolov7_640_val
```
### Evaluation
We can evaluate the performance of our custom training using the provided evalution script
```
!python detect.py --weights runs/train/exp/weights/best.pt --conf 0.1 --source {dataset.location}/test/images

```

### Inference

On video : 

```
python detect.py --weights yolov7.pt --conf 0.25 --img-size 640 --source yourvideo.mp4
```

On image:
```
python detect.py --weights yolov7.pt --conf 0.25 --img-size 640 --source inference/images/horses.jpg
```
