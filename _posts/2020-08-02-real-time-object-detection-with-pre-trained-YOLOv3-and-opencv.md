---
layout: post
title:  "Real-Time Object Detection with pre-trained YOLOv3 and OpenCV"
date:   2020-08-01 12:00:00
---

## Goal

In this article, we will perform real-time object detection with YOLOv3 (You Only Look Once) which is the current state of the art, real time object detection system. I want to reference .

## Topics
1. [How YOLO works](#how-yolo-works)
2. [What YOLO can detect](#what-YOLO-can-detect)
3. [Concept of Transfer Learning](#concept-of-transfer-learning)
4. [How to install YOLO](#how-to-install-yolo)
5. [Code](#code)
6. [Output](#output)

## How YOLO works

Traditional, R-CNN family of algorithms uses regions to localize the objects in images. High scoring regions of the image are considered as object detected.

YOLO follows a completely different approach. It applies a neural network to the entire image to predict bounding boxes and probability of being some object. High probabilities of the image are considered as object detected.

## What YOLO can detect

YOLO can be applied to:
1. Image File
2. Webcam feed
3. Video file

Pre-trained YOLOv3 can detect 80 objects, such as:
1. Person
2. Bicycle
3. Car

## Concept of Transfer Learning

Transfer learning is a technique to reuse the weights in one or more layers from a pre-trained network model in a new model by:
1. Keeping the weights
2. Fine tuning the weights
3. Adapting the weights entirely when training a new model


## How to install YOLO

1. Create a folder. I will name my folder Object-Detection-YOLOv3.
2. Download weight file and configuration file based on the frames per second (FPS) or mean Average Precision (mAP) from [pjreddie](https://pjreddie.com/darknet/yolo/) and place it in the Object-Detection-YOLOv3 folder.

![enter image description here](https://3.bp.blogspot.com/-_bSVPHpHPDE/Xybada5Lh_I/AAAAAAAAJqA/Pk-c1lfrJcI6Y2pya4SY--B-v9tSLwTNACLcBGAsYHQ/s1600/YOLOv3.png)

3. Download name file - coco from [github](https://github.com/pjreddie/darknet/blob/master/data/coco.names) and place it in the Object-Detection-YOLOv3 folder.
4. Install OpenCV 3.4.2 or above `pip install opencv-python`

## Code

```python
import cv2
import numpy as np

net = cv2.dnn.readNet('yolov3.weights', 'yolov3.cfg')
classes = []

with open('coco.names', 'r') as f:
    classes = f.read().splitlines()

#print(classes)

img = cv2.imread('image.jpg')
height, width, _ = img.shape

# cv2.imshow('Image', img)
# cv2.waitKey(0)
# cv2.destroyAllWindows()

blob = cv2.dnn.blobFromImage(img, 1/255, (416, 416), (0, 0, 0), swapRB=True, crop=False)

# for b in blob:
#     for n, img_blob in enumerate(b):
#         cv2.imshow(str(n), img_blob)
#         cv2.waitKey(0)

net.setInput(blob)
output_layers_names = net.getUnconnectedOutLayersNames()
layerOutputs = net.forward(output_layers_names)

boxes = []
confidences = []
class_ids = []

for output in layerOutputs:
    for detection in output:
        scores = detection[5:]
        class_id = np.argmax(scores)
        confidence = scores[class_id]

        if (confidence > 0.5):
            center_x = int(detection[0]*width)
            center_y = int(detection[1]*height)
            w = int(detection[2]*width)
            h = int(detection[3]*height)

            x = int(center_x - w/2)
            y = int(center_y - h/2)

            boxes.append([x, y, w, h])
            confidences.append(float(confidence))
            class_ids.append(class_id)
            
# print(type(boxes))
# print(type(confidences))
# print(boxes)
# print(confidences)

indexes = cv2.dnn.NMSBoxes(boxes, confidences, 0.5, 0.4)
# print(indexes.flatten())

font = cv2.FONT_HERSHEY_PLAIN
colors = np.random.uniform(0, 255, size=(len(boxes), 3))

for i in indexes.flatten():
    x, y, w, h = boxes[i]
    label = str(classes[class_ids[i]])
    confidence = str(round(confidences[i], 2))
    color = colors[i]
    cv2.rectangle(img, (x,y), (x+w, y+h), color, 2)
    cv2.putText(img, label + " " + confidence, (x, y+20), font, 2, (255,255,255), 2)

cv2.imshow('Image', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

## Output

![Detection](https://2.bp.blogspot.com/-plFESxyTjdY/XybtJZxvLMI/AAAAAAAAJqM/4J23JnOUF7Yiez1T4UWiQaLBalDA_iT8gCLcBGAsYHQ/s1600/Detection.png)






