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
