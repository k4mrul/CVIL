
***Detection Pipeline Fundamentals***

Object detection identifies what objects are present in an image and where they are located. For example, YOLO can detect a cat in an image, label it as “cat,” and draw a bounding box around it.

**Classification vs. Localization**

Classification predicts the object’s class, such as cat, car, or person. It tells us what is in the image but not where it is.

Localization predicts the object’s position using a bounding box. The box is usually represented by coordinates such as its center position, width, and height.

For example, classification says, “This image contains a dog.” Localization says, “The dog is inside this rectangular area.” Object detection combines both tasks.

**Anchor Boxes**

Anchor boxes are predefined bounding-box shapes that help a model detect objects with different sizes and aspect ratios. Some anchors may be tall and narrow, while others may be short and wide.

For example, a tall anchor box may match a standing person, while a wide anchor box may match a car. During training, the model adjusts the most suitable anchor box to fit the actual object.

Newer YOLO versions may use anchor-free detection, where the model predicts objects without predefined anchor boxes.

**Intersection over Union (IoU)**

Intersection over Union, or IoU, measures how much a predicted bounding box overlaps with the correct bounding box.

It is calculated as:
```
IoU = Overlapping Area / Combined Area
```

For example, if a predicted box closely matches the actual box, its IoU might be 0.85. If the boxes barely overlap, the IoU might be 0.20. A higher IoU means more accurate localization.

**Non-Maximum Suppression (NMS)**

A model may predict several overlapping boxes for the same object. Non-Maximum Suppression, or NMS, removes these duplicate predictions.

For example, YOLO might produce three boxes around the same car with confidence scores of 0.90, 0.75, and 0.60. NMS keeps the strongest box and removes the weaker overlapping boxes.

**Confidence Scores**

A confidence score represents how certain the model is that a bounding box contains a valid object. It is commonly based on both the probability that an object exists and the predicted class probability.

For example:
```
Person: 0.92
Car: 0.81
Dog: 0.43
```

The model is very confident about the person and car, but less confident about the dog. A confidence threshold, such as 0.50, can be used to remove weak predictions.

**Two-Stage vs. One-Stage Detectors**
- Two-stage: R-CNN, Fast R-CNN, Faster R-CNN (proposal generation, accuracy-focused)
- One-stage: SSD, RetinaNet, YOLO (real-time inference)

**RetinaNet**
- Focal loss: class imbalance, hard example emphasis

**YOLO Evolution**
- YOLOv1: unified detection, grid prediction
- YOLOv2: anchors, batch norm
- YOLOv3: multi-scale detection, Darknet-53
- YOLOv4 / v5: engineering optimizations
- YOLOX: anchor-free
- YOLOv8+: decoupled heads, modern training

**Must-Know YOLO Internals**
- Backbone
- Neck
- Head
- PAN / FPN
- CSP blocks
- Anchor-based vs. anchor-free
- Label assignment
- NMS
- CIoU / GIoU / DIoU losses

**Detection Metrics**
- mAP@0.5
- mAP@0.5:0.95
- Precision-recall curves
