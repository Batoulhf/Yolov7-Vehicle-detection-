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
![Image](https://github.com/Batoulhf/Yolov7-Vehicle-detection-/blob/main/Detection%20results/test/Metrics/test_labels.jpg)

### Evaluation
We can evaluate the performance of our custom training using the provided evalution script
```
!python detect.py --weights runs/train/exp/weights/best.pt --conf 0.1 --source {dataset.location}/test/images

```

```
!python test.py --data data.yaml --img 640 --batch 32 --conf 0.001 --iou 0.65 --device 0 --weights runs/train/exp/weights/best.pt 
```
#### Performance table
| Class      | Precision | Recall | mAP@.5 |
| :----------|:---------:|:------:|-------:|
| All        | 0.93      | 0.97   | 0.98   |
| Bus        | 0.97      | 1      | 0.99   |
| Car        | 0.89      | 0.96   | 0.97   |
| Motorcycle | 0.87      | 1      | 0.98   |
| Truck      | 0.93      | 0.95   | 0.98   |
| Van        | 0.99      | 0.96   | 0.99   |


### Inference

On video : 

```
python detect.py --weights yolov7.pt --conf 0.25 --img-size 640 --source yourvideo.mp4
```
![Video](https://github.com/Batoulhf/Yolov7-Vehicle-detection-/blob/main/Detection%20results/detect/Video/vid3_Trim_Trim%20(1).gif)

On image:
```
python detect.py --weights yolov7.pt --conf 0.25 --img-size 640 --source yourimage.jpg
```

![Image](https://github.com/Batoulhf/Yolov7-Vehicle-detection-/blob/main/Detection%20results/detect/Images/image291_jpg.rf.83ec2f34acfb6f568d1bf4c7f66dc26f.jpg))
![Image2](https://github.com/Batoulhf/Yolov7-Vehicle-detection-/blob/main/Detection%20results/detect/Images/B-1080p--26-_jpg.rf.83d7cf8e213fe2829303613e735aa3ce.jpg)

## Confustion matrix
The performance results of our algorithm are supported by this matrix, it represents numbers from predicted and actual values. The diagonal elements represent the number of points for which the predicted label is equal to the actual label. It can be seen that the diagonal values are high, indicating many correct predictions. While the off-diagonal ”FP and FN” elements are the mislabeled ones. the false positive value ≪ FP ≫ indicates the number of actual negative examples classified as positive, and the false negative value ≪ FN ≫ is the number of actual positive examples classified as negative.

![Image](https://github.com/Batoulhf/Yolov7-Vehicle-detection-/blob/main/Detection%20results/test/Metrics/confusion_matrix.png)
