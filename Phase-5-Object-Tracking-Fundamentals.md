# Object Tracking Fundamentals 

Think of **object tracking** as:

> "I found a person/car in one video frame. Now I want to keep following the same object in the next frames."

---

# Tracking Paradigms

## 1. Online Tracking
- Tracks objects **live while the video is running**.
- Fast and used in real-time systems.

**Example:** CCTV following a person in real time.

## 2. Offline Tracking
- Has access to the **entire video first**.
- More accurate but slower.

**Example:** Analysing a recorded football match.

## 3. Detection-Based Tracking
- First detects objects.
- Then tracks them across frames.

```text
Detect → Track → Detect → Track
```

---

# Kalman Filter

A smart predictor that guesses where an object will be next.

## 1. Prediction Step
Predict the next location.

**Example:**

```text
Current position = x=100
Moving right

Predicted next position = x=110
```

## 2. Update Step
Compare prediction with actual detection and correct it.

```text
Predicted = x=110
Actual = x=108

Update prediction
```

## 3. Uncertainty Modeling
Measures how sure the tracker is.

- Low uncertainty = confident ✅
- High uncertainty = not confident ⚠️

## 4. State Vector

Stores object information:

```text
x        = horizontal position
y        = vertical position
velocity = speed + direction
bbox     = bounding box size
```

---

# Hungarian Algorithm

## Minimum Cost Matching

Matches tracked objects to new detections with the smallest error.

Example:

```text
Track A → Detection A
Track B → Detection B
Track C → Detection C
```

Chooses the best overall matching.

---

# SORT

**SORT = Simple Online Realtime Tracking**

Pipeline:

```text
Detect
   ↓
Kalman Predict
   ↓
IoU Match
   ↓
Hungarian Assignment
```

## IoU Match

**IoU (Intersection over Union)** measures how much two bounding boxes overlap.

```text
More overlap = likely same object
Less overlap = likely different object
```

### Why SORT?

- Fast ✅
- Simple ✅
- Real-time ✅

---

# DeepSORT

Improved version of SORT.

Uses:

1. Motion
2. Appearance

## Motion + Appearance Fusion

Instead of only checking position, it also checks appearance.

```text
Where is it?
+
What does it look like?
```

## Appearance Embeddings (ReID)

Creates a feature vector describing appearance.

Example:

```text
Red shirt
Blue jeans
Backpack
```

Even if the person disappears and returns, DeepSORT can recognize them.

---

# ByteTrack

## Keep Low-Confidence Detections

Most trackers discard weak detections.

```text
Confidence = 0.30

Other trackers → discard
ByteTrack → keep
```

Useful when:
- Object is partially hidden
- Lighting is poor
- Detection confidence is low

## Association-First Philosophy

```text
Match first
Remove mistakes later
```

Result:

- Fewer lost tracks ✅
- Better tracking ✅

---

# BoT-SORT

Enhanced ByteTrack.

## ReID-Enhanced Tracking

Uses appearance features to keep identities correct.

Example:

```text
Person A and Person B cross paths
```

Some trackers may swap IDs.

BoT-SORT checks appearance and prevents ID swaps.

---

# Tracking Metrics

Used to measure tracker performance.

## 1. MOTA

**Multiple Object Tracking Accuracy**

Measures overall tracking quality.

```text
Higher MOTA = Better
```

---

## 2. IDF1

Measures identity consistency.

Example:

```text
Person #5 stays Person #5
```

```text
Higher IDF1 = Better
```

---

## 3. HOTA

Measures both:

- Detection quality
- Tracking quality

```text
Higher HOTA = Better
```

---

## 4. ID Switches

Counts incorrect identity changes.

Example:

```text
Frame 1:
Person A = ID 1

Frame 20:
Person A = ID 7
```

This is an ID switch ❌

```text
Lower ID Switches = Better
```

---

# 30-Second Revision

```text
Kalman Filter  = Predict next position
Hungarian Algo = Match tracks to detections

SORT           = Kalman + IoU + Hungarian
DeepSORT       = SORT + Appearance Features
ByteTrack      = Keeps Low-Confidence Detections
BoT-SORT       = ByteTrack + ReID

MOTA           = Overall Accuracy
IDF1           = Identity Consistency
HOTA           = Detection + Tracking Quality
ID Switches    = Wrong Identity Changes
```

## Easy Memory Trick

```text
Kalman    = Predict
Hungarian = Match

SORT      = Fast
DeepSORT  = SORT + Looks
ByteTrack = Keeps Weak Detections
BoT-SORT  = ByteTrack + Looks
```
# Specialization Tracks

## What is Person ReID (Person Re-Identification)?

ReID (Person Re-Identification) means:

> "Given a person image, find the same person from other cameras or images."

### Example

Camera 1:

```text
Person wearing:
- Red shirt
- Blue jeans
- Backpack
```

Camera 2:

```text
Many people appear.
Find the same person.
```

ReID tries to answer:

```text
"Is this the same person?"
```

Unlike tracking, ReID works even when:

- The person disappears
- The camera changes
- There is a time gap

---

# Why ReID is Important

Used in:

- Multi-camera surveillance
- Smart cities
- Retail analytics
- Airport monitoring
- Tracking people across cameras

Example:

```text
Camera A → Person enters building

30 minutes later

Camera B → Same person exits building
```

ReID identifies them as the same person.

---

# ReID Pipeline

Typical workflow:

```text
Detector
   ↓
Crop Person
   ↓
Embedding Network
   ↓
Feature Comparison
   ↓
Retrieval / Matching
```

## 1. Detector

Detect people in an image.

Examples:

```text
YOLO
Faster R-CNN
RT-DETR
```

Output:

```text
Bounding boxes around people
```

---

## 2. Crop Person

Cut out each detected person.

```text
Original Image
      ↓
Person Crop
```

Only the person image is used.

---

## 3. Embedding Network

Convert the person image into numbers.

Example:

```text
Person Image
      ↓
[0.23, 0.81, 0.12, ...]
```

This vector is called an **embedding**.

Think of it as:

> A fingerprint for appearance.

---

## 4. Feature Comparison

Compare embeddings.

Example:

```text
Person A = [1,2,3]

Person B = [1.1,2.1,2.9]
```

Very similar → same person likely.

---

## 5. Retrieval / Matching

Search database for the closest embeddings.

```text
Query Person
      ↓
Find most similar people
```

---

# Embedding Learning

Goal:

```text
Same person → embeddings close together

Different people → embeddings far apart
```

---

## 1. Triplet Loss

Uses three images:

```text
Anchor
Positive
Negative
```

### Anchor

Reference image.

### Positive

Same person.

### Negative

Different person.

Example:

```text
Anchor   = Person A
Positive = Person A
Negative = Person B
```

Training goal:

```text
Anchor closer to Positive

Anchor farther from Negative
```

### Margin

Minimum required distance.

```text
Different identities should be
at least X distance apart.
```

### Hard Mining

Choose difficult examples.

Example:

```text
Negative looks very similar
to Anchor
```

These difficult examples help training more.

---

## 2. Contrastive Loss

Uses pairs.

```text
Same person
→ Pull together

Different people
→ Push apart
```

Simple version of metric learning.

---

## 3. ArcFace / CosFace / Circle Loss

Improved methods for separating identities.

Idea:

```text
Make identity boundaries clearer.
```

Result:

```text
Person A embeddings
and
Person B embeddings

become easier to separate.
```

---

# ReID Architectures

## 1. ResNet50 Baseline

Most common starter model.

```text
Simple
Strong
Widely used
```

If you're learning ReID:

```text
Start here.
```

---

## 2. PCB

PCB = Part-based Convolutional Baseline

Idea:

```text
Head
Chest
Legs
Shoes
```

Look at body parts separately.

Useful when some parts are hidden.

---

## 3. MGN

MGN = Multi-Granularity Network

Looks at:

```text
Whole body
+
Body parts
```

Usually better accuracy than basic ResNet50.

---

## 4. TransReID

Transformer-based ReID model.

Uses attention.

```text
Focus on important body regions
automatically.
```

---

## 5. ViT-Based ReID

ViT = Vision Transformer.

Modern approach:

```text
Image
    ↓
Transformer
    ↓
Embedding
```

Often among the best-performing models today.

---

# ReID Tricks

Small improvements that can significantly increase accuracy.

---

## 1. Label Smoothing

Instead of:

```text
100% sure this is Person A
```

Use:

```text
95% Person A
5% uncertainty
```

Helps prevent overfitting.

---

## 2. Random Erasing

Randomly hide part of an image during training.

Example:

```text
Backpack removed
```

Model learns to rely on more features.

Result:

```text
More robust model
```

---

## 3. Center Loss

Pull embeddings of the same identity closer together.

```text
Person A images
      ↓
Compact cluster
```

---

## 4. BNNeck

A special Batch Normalization layer.

Very common in modern ReID systems.

Benefits:

```text
Better training
Better retrieval
```

---

## 5. Re-ranking

After initial search:

```text
Top matches found
       ↓
Refine ranking
```

Often boosts final accuracy.

---

## 6. Hard Mining

Use difficult examples.

Example:

```text
Two people wearing
almost identical clothes
```

Model learns to distinguish them.

---

## 7. Camera-Aware Training

Different cameras have:

```text
Different lighting
Different angles
Different colours
```

Train model to handle these differences.

---

# ReID Metrics

Used to evaluate performance.

---

## 1. Rank-1 Accuracy

Most important ReID metric.

Question:

```text
Is the first returned person
the correct one?
```

Example:

```text
Query → Search

Top result = correct person
```

Success ✅

---

## 2. mAP

mAP = Mean Average Precision

Measures overall retrieval quality.

Example:

```text
Top 10 retrieved results

How many are correct?
How highly are they ranked?
```

Higher is better.

---

# Self-Supervised ReID

Train with little or no labels.

---

## 1. CLIP Features

CLIP learns visual representations from huge image-text datasets.

For ReID:

```text
Image
   ↓
CLIP Embedding
   ↓
Compare Features
```

Often works surprisingly well without ReID training.

---

## 2. DINO Features

Self-supervised vision model.

Learns useful representations without manual labels.

```text
Image
   ↓
DINO Features
   ↓
Similarity Search
```

---

## 3. Unsupervised / Domain-Adaptive ReID

Problem:

```text
Model trained on Dataset A

Used on Dataset B
```

Different cameras and environments may reduce performance.

Solution:

```text
Adapt model to new domain
without many labels.
```

---

# 30-Second Revision

```text
ReID = Find the same person across images/cameras.

Pipeline:
Detect
 → Crop
 → Embed
 → Compare
 → Match

Triplet Loss:
Anchor
Positive
Negative

ResNet50 = Basic ReID model
PCB      = Body parts
MGN      = Multi-scale/body parts
TransReID= Transformer ReID
ViT ReID = Vision Transformer ReID

Rank-1 = Is top match correct?
mAP    = Overall retrieval quality

CLIP = Large-scale image-text features
DINO = Self-supervised features

Key Goal:
Same person → close embeddings
Different people → far embeddings
```

## Easy Memory Trick

```text
Tracking = Follow a person in video

ReID = Find the same person
       across cameras

Kalman = Predict
Hungarian = Match

DeepSORT / BoT-SORT
          ↓
Use ReID features internally
to keep identities consistent
```
