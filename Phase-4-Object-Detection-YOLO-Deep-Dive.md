
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

Object detection models are commonly divided into two-stage detectors and one-stage detectors. The main difference is how they find and classify objects.

- Two-Stage Detectors

  Two-stage detectors first generate region proposals, which are possible areas containing objects. In the second stage, they classify each proposed region and refine its bounding box.

  Examples include R-CNN, Fast R-CNN, and Faster R-CNN. These models are generally accurate, but their multiple processing stages can make them slower.

  For example, Faster R-CNN first finds possible locations of cars in an image. It then examines each location to confirm whether it contains a car and adjusts the bounding box.

- One-Stage Detectors

  One-stage detectors predict object classes and bounding boxes in a single pass through the model. They do not use a separate region-proposal stage.

  Examples include SSD, RetinaNet, and YOLO. These models are usually faster and are suitable for real-time applications.

  For example, YOLO processes a video frame once and directly predicts the locations and classes of people, cars, and other objects.

- Simple Comparison

  Two-stage detectors mainly focus on high accuracy, while one-stage detectors mainly focus on high speed and real-time inference. However, modern one-stage detectors such as YOLO can provide both strong accuracy and fast performance.


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
- **Backbone** → Extracts image features (e.g., learns wheels, windows, and edges of a car).
- **Neck** → Combines features from different layers (e.g., helps YOLO detect both small and large cars).
- **Head** → Makes final predictions: class, bounding box, and confidence (e.g., Car, 96%, box coordinates).
- **PAN/FPN** → **FPN (Feature Pyramid Network)** and **PAN (Path Aggregation Network)** help detect objects at different scales (e.g., a far person and a nearby truck).
- **CSP Blocks** → Make YOLO faster and more efficient by splitting and merging feature paths.
- **Anchor-Based** → Uses predefined box shapes (e.g., 20×20, 50×50 anchors). Used in older YOLO versions.
- **Anchor-Free** → Predicts object locations directly (e.g., finds a car's center and size without anchors). Used in newer YOLO versions (YOLOv8+).
- **Label Assignment** → During training, YOLO decides which prediction should learn which object. It matches predictions to ground truth (e.g., a box with IoU = 0.8 learns the car).
- **NMS (Non-Maximum Suppression)** → Removes duplicate detections (e.g., keeps Car 95%, removes Car 92% and 89%).
- **GIoU Loss** → Measures overlap and empty space between predicted and actual boxes.
- **DIoU Loss** → Measures overlap plus center-point distance.
- **CIoU Loss** → Measures overlap, center distance, and aspect ratio. Usually the most complete loss.

**Detection Metrics**

- **mAP@0.5** → A prediction is considered correct if **IoU ≥ 0.5** (e.g., IoU = 0.7 counts as correct). Higher mAP@0.5 means better detection performance.
- **mAP@0.5:0.95** → Average mAP across IoU thresholds from **0.50 to 0.95**. More strict and realistic because it evaluates both object detection and bounding box precision.

**YOLO Pipeline**

```text
Image
  ↓
Backbone
  ↓
Neck (PAN/FPN)
  ↓
Head
  ↓
Predictions
  ↓
NMS
  ↓
Final Detections
```

**Quick Interview Summary**

```text
Backbone         = Feature extraction
Neck             = Feature fusion
Head             = Object prediction
PAN/FPN          = Multi-scale detection
CSP Blocks       = Efficiency and speed
Anchor-Based     = Uses predefined anchors
Anchor-Free      = Direct box prediction
Label Assignment = Match predictions with ground truth
NMS              = Remove duplicate detections
GIoU             = Overlap + empty space loss
DIoU             = Overlap + center distance loss
CIoU             = Overlap + distance + shape loss
mAP@0.5          = Detection accuracy (IoU ≥ 0.5)
mAP@0.5:0.95     = Stricter overall detection accuracy
```


