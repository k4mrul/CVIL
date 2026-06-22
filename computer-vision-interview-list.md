# Computer Vision Interview List

A topic-by-topic checklist for studying and revising computer vision fundamentals before an ML/CV interview, from core math up through deployment.

This is meant as a **map, not a textbook**: it tells you what to look up, not how. Pair it with your own sources (papers, blog posts, courses, whatever clicks for you) and use it to track what you've actually internalized versus what's still a gap.

> **On pacing:** the phase numbers are a suggested order of attack, not a fixed schedule... stretch them over a week, a month, or however long you've got.

The checklist is split into two parts:

- **Core Phases (1-5)**: math, CNNs, Transformers, detection, and tracking. Relevant to almost any computer vision role.
- **Specialization Tracks**: deep dives into specific tracks (ReID, Deployment, and more to come). Pick the ones that match the role you're interviewing for.

---

## Phase 1: Core Math & Statistics

**Probability & Statistics**
- Bayes' theorem
- Conditional probability
- Likelihood vs. probability
- Maximum likelihood estimation (MLE)
- MAP estimation
- Gaussian distributions
- Covariance matrices
- Correlation vs. covariance
- Bias-variance tradeoff
- Entropy & cross-entropy
- KL divergence
- Expectation & variance
- Hypothesis testing basics
- Precision / Recall / F1
- ROC / AUC
- Calibration

**Cross Entropy: Know the "Why"**
- Why log is used
- Why one-hot labels work
- Why cross-entropy pairs naturally with softmax
- Why cross-entropy punishes confident wrong predictions heavily

**Optimization**
- Gradient descent
- SGD
- Momentum
- Adam
- AdamW
- Weight decay
- Learning rate schedules
- Cosine annealing
- Warmup
- Vanishing gradients
- Exploding gradients
- Backpropagation & the chain rule

**Why Residual Connections Help Gradients**
- Identity shortcut preserves gradient flow
- Avoids deep-network degradation
- Creates an easier optimization landscape

---

## Phase 2: CNNs From First Principles

**Core CNN Concepts**         
- Convolution
- Kernels
- Receptive fields
- Padding
- Stride
- Dilation
- Pooling
- Feature hierarchies
- Translation invariance

**Why Convolutions Are Parameter-Efficient**
- Local connectivity
- Weight sharing
- Spatial inductive bias

**CNN Architecture Evolution**
- LeNet: first practical CNN
- AlexNet: ReLU, GPU training, dropout, ImageNet breakthrough
- VGG: simplicity, stacked 3×3 convolutions
- GoogLeNet / Inception: multi-scale processing
- ResNet: residual learning, degradation problem, skip connections, identity mappings
- DenseNet: feature reuse, gradient flow
- EfficientNet: compound scaling
- ConvNeXt: CNNs modernized with Transformer-era design

**Must-Know CNN Topics**
- BatchNorm
- LayerNorm
- GroupNorm
- Dropout
- Residual blocks
- Depthwise separable convolution
- MobileNet
- Squeeze-and-Excitation
- FPN (Feature Pyramid Networks)

---

## Phase 3: Transformers & Vision Transformers

**Transformer Fundamentals**
- Self-attention: queries, keys, values, similarity matching, scaling, softmax
- Multi-head attention: parallel subspace learning, diverse representations
- Positional encoding: why Transformers need spatial order injected

**Vision Transformers (ViTs)**
- Core idea: image → patches → tokens
- Patch embedding
- CLS token
- ViT encoder
- Why ViTs need huge datasets

**Key ViT Variants & Models**
- DeiT
- Swin Transformer
- MAE
- DINO
- DINOv2
- CLIP
- Segment Anything (SAM)

**Self-Supervised Learning**
- Contrastive learning
- Positive / negative pairs
- Momentum encoders
- Teacher-student learning

**CLIP**
- Image-text alignment
- Zero-shot classification
- Embedding space learning

**DINO / DINOv2**
- Self-distillation
- Label-free representation learning
- Strong embeddings

---

## Phase 4: Object Detection & YOLO Deep Dive

**Detection Pipeline Fundamentals**
- Classification vs. localization
- Anchor boxes
- IoU
- NMS
- Confidence scores

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

---

## Phase 5: Object Tracking Fundamentals

**Tracking Paradigms**
- Online vs. offline tracking
- Detection-based tracking

**Kalman Filter**
- Prediction step
- Update step
- Uncertainty modeling
- State vector: x, y, velocity, bbox

**Hungarian Algorithm**
- Minimum cost matching

**SORT**
- Detect → Kalman predict → IoU match → Hungarian assignment

**DeepSORT**
- Motion + appearance fusion
- Appearance embeddings bridge into ReID

**ByteTrack**
- Keep low-confidence detections
- Association-first philosophy

**BoT-SORT**
- ReID-enhanced tracking

**Tracking Metrics**
- MOTA
- IDF1
- HOTA
- ID switches

---

## Specialization Tracks

Pick the track(s) relevant to your target role. Each one assumes the Core Phases above as a foundation.

---

### Specialization: Person Re-Identification (ReID)

**What Is Person ReID?**
- Learning identity-consistent embeddings across cameras/views
- Metric learning, retrieval, representation learning

**ReID Pipeline**
- Detector
- Crop person
- Embedding network
- Feature comparison
- Retrieval / matching

**Embedding Learning**
- Triplet loss: anchor, positive, negative, margin, hard mining
- Contrastive loss
- Circle loss / ArcFace / CosFace: angular margins for identity separation

**ReID Architectures**
- ResNet50 baseline
- PCB
- MGN
- TransReID
- ViT-based ReID

**ReID Tricks**
- Label smoothing
- Random erasing
- Center loss
- BNNeck
- Re-ranking
- Hard mining
- Camera-aware training

**ReID Datasets**
- Market-1501
- DukeMTMC
- MSMT17

**ReID Metrics**
- Rank-1 accuracy
- mAP

**Self-Supervised ReID**
- CLIP features
- DINO features
- Unsupervised / domain-adaptive ReID

---

### Specialization: Deployment & Production CV

**Model Optimization**
- FP16
- INT8 quantization
- TensorRT
- ONNX
- Pruning
- Distillation

**Inference Optimization**
- Batching
- Async inference
- CUDA streams
- Memory bottlenecks

**Edge Deployment**
- Jetson devices
- TensorRT engines
- DeepStream basics

**Production Tracking/ReID Systems**
- Camera stream → detector → tracker → ReID embeddings → identity DB → retrieval/search

**System Design Questions**
- Camera synchronization
- Embedding database
- Temporal consistency
- Latency constraints
- Distributed inference
- Edge/cloud tradeoffs

---

### Specialization: _Your Track Here_

More specialization tracks (Segmentation, OCR, 3D Vision, VLMs, LLMs, and others) are planned. See the [Contributing](#contributing) section below if you'd like to help add one.

---

## Final Interview Advice

For every topic on this list, push past "I've heard of it" and be able to answer:

- **Why** does this method exist?
- **What** limitation did it solve?
- **What** tradeoff did it introduce?

For each one, aim to know: the **intuition**, the **equations**, the **architecture**, the **tradeoffs**, the **failure cases**, and the **modern successors**.

---

## Contributing

This checklist covers the core path plus two specialization tracks (ReID, Deployment), but computer vision is bigger than that. If you work in (or are studying for) a track that isn't here yet, contributions are welcome.

### Adding a new specialization track

1. **Open an issue first** describing the specialization you want to add (e.g. *Segmentation*, *OCR*, *3D Vision*, *VLMs*, *LLMs for CV*, *Video Understanding*, etc.), so it can be discussed before you put in the work.
2. Once it's greenlit, submit a PR that:
   - Follows the same structure as the existing tracks: a short "what is this?" framing, then grouped sub-lists (concepts → architectures/models → metrics/tricks → datasets, as relevant).
   - Stays at **checklist depth**: topic names and short framing phrases, not full explanations. The goal is to point at what to study, not to teach it inline.
   - Slots in under **Specialization Tracks**, replacing or sitting alongside the `_Your Track Here_` placeholder.
3. Keep tone and formatting consistent with the rest of the doc (heading levels, bullet style, no checkboxes).

### Other contributions

- Spotted an outdated reference, a missing must-know model, or a topic that's drifted out of relevance? Open an issue or PR.
- Disagree with how something is categorized (Core vs. Specialization)? Open an issue, happy to discuss.

### Ideas for future tracks

Segmentation • OCR • 3D Vision / Point Clouds • VLMs • LLMs for CV • Video Understanding • Generative Models (Diffusion/GANs) • Medical Imaging • Pose Estimation

---

*Found this useful? Star it, fork it, and help make it bigger.*
