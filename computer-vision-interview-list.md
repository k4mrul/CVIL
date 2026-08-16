# Computer Vision Interview List

A topic-by-topic checklist for studying and revising computer vision fundamentals before an ML/CV interview, from core math up through deployment.

This is meant as a **map, not a textbook**: it tells you what to look up, not how. Pair it with your own sources (papers, blog posts, courses, whatever clicks for you) and use it to track what you've actually internalized versus what's still a gap.

> **On pacing:** the phase numbers are a suggested order of attack, not a fixed schedule... stretch them over a week, a month, or however long you've got.

The checklist is split into two parts:

- **Core Phases (1-5)**: math, CNNs, Transformers, detection, and tracking. Relevant to almost any computer vision role.
- **Specialization Tracks**: deep dives into specific tracks (ReID, Deployment, and more to come). Pick the ones that match the role you're interviewing for.

---

## [Phase 1: Core Math & Statistics](https://github.com/k4mrul/CVIL/blob/main/Phase-1:-Core-Math-Statistics.md)
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
  
[**Cross Entropy: Know the "Why"**](https://github.com/k4mrul/CVIL/blob/main/cross-entropy.md)
- Why log is used
- Why one-hot labels work
- Why cross-entropy pairs naturally with softmax
- Why cross-entropy punishes confident wrong predictions heavily

[**Optimization**](https://github.com/k4mrul/CVIL/blob/main/optimization.md)
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

Very deep networks can have trouble sending gradients back to earlier layers. As a result, those layers learn slowly or stop learning.

A residual connection creates a shortcut:

```
Output = learned change + original input
Output = F(x) + x
```

The shortcut lets the gradient travel backward more easily.

Simple Example

Suppose the input is 10, and the desired output is 12.
Instead of learning the complete transformation from 10 to 12, the network only learns the difference:

```
Learned change = 2
Output = 10 + 2 = 12
```

So, residual connections help deep networks by:
- Keeping gradients flowing
- Preventing learning from getting worse as layers are added
- Letting layers learn small changes instead of complete transformations

---

## Phase 2: CNNs From First Principles
[**Core CNN Concepts**](https://github.com/k4mrul/CVIL/blob/main/phase2-CoreCNNConcepts.md)
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

Convolutional layers use fewer parameters than fully connected layers because they process images using small filters instead of connecting every input pixel to every output neuron. 

- Local connectivity:

  A convolutional neuron connects only to a small local region of the input, called its receptive field. This works well because nearby pixels are usually more related than distant pixels. Example: A 3 × 3 filter examines only 9 pixels at a time, rather than connecting to every pixel in the image

- Weight sharing:

  The same filter weights are reused across the entire image. Therefore, a filter that detects an edge in one location can detect the same edge anywhere else. Example: A 3 × 3 filter has only 9 weights, plus one bias. These same parameters are applied at the top, middle, and bottom of the image.

- Spatial inductive bias: 

  Convolutions assume that spatial patterns are meaningful and that useful features can appear in different locations. This built-in assumption helps the model learn image features efficiently. Example: A filter trained to detect a cat’s ear can recognize that shape whether it appears on the left or right side of an image.

So convolutions are parameter-efficient because they use small local connections, reuse the same weights, and include assumptions that naturally match the spatial structure of images.

**CNN Architecture Evolution**
- LeNet (1998): First practical CNN using convolution and pooling layers for image recognition.

  Example: Recognizing handwritten digits (0-9) on bank checks.
- AlexNet (2012): Introduced ReLU, GPU training, and dropout, achieving a breakthrough on ImageNet.

  Example: Distinguishing between images of cats, dogs, and cars with much higher accuracy.
- VGG (2014): Used a simple design with many stacked 3×3 convolution layers to learn deeper features.

  Example: Detecting edges → shapes → objects (e.g., identifying a bicycle in a photo).
- GoogLeNet / Inception (2014): Applied multi-scale processing by using different filter sizes simultaneously.

  Example: Detecting both small traffic signs and large buildings in the same image.
- ResNet (2015): Introduced skip connections and residual learning to train very deep networks effectively.

  Example: A 152-layer network recognizing thousands of object categories without performance degradation.
- DenseNet (2017): Connected every layer to later layers for feature reuse and better gradient flow.

  Example: Early edge features are reused directly for face or animal recognition.
- EfficientNet (2019): Used compound scaling to balance depth, width, and image resolution efficiently.

  Example: High-accuracy image classification on mobile devices with fewer parameters.
- ConvNeXt (2022): Modernized CNNs using ideas inspired by Transformers while keeping convolution operations.

  Example: Achieving Transformer-level image recognition performance with a CNN-based model.


**Must-Know CNN Topics**

Normalization transforms/scales data into a standard form that is easier for a neural network to learn from. Normalization makes data more consistent by reducing large differences between values.

Without normalization, some features may have very large values while others have small values. This can make training unstable and slow.

Exmaple: pixel values of an image are: [0, 128, 255]. We can normalize them to the range 0 to 1 by dividing by 255:  [0.0, 0.5, 1.0]

1. Batch Normalization: Batch Normalization normalizes the output of a layer using the mean and variance of a mini-batch. This makes training faster and more stable because the network receives values in a more consistent range. It also allows the model to use higher learning rates and can reduce the need for Dropout in some cases.
   
   Example: In a CNN that classifies cats and dogs, BatchNorm can be added after a convolution layer so that the feature values do not become too large or too small during training.

3. Layer Normalization: Layer Normalization normalizes the features inside one single sample instead of using the whole batch. It does not depend on batch size, so it works well when the batch size is very small. It is more common in Transformers and RNNs, but the idea is still useful to understand for deep learning. 

    Example: If one image passes through a network, LayerNorm normalizes the features of that image only, instead of comparing it with other images in the batch.

3. Group Normalization: Group Normalization divides the channels of a feature map into smaller groups and normalizes each group separately. It is useful when the batch size is small, where BatchNorm may not work well.

    Example: Suppose a CNN layer has 32 channels. GroupNorm can divide them into 4 groups, with 8 channels in each group, and normalize each group separately.

4. Dropout: Dropout is a regularization technique that randomly turns off some neurons during training. This helps the model avoid depending too much on specific neurons and reduces overfitting.

    Example: If a layer has 100 neurons and Dropout rate is 0.5, then around 50 neurons are randomly ignored during one training step. This forces the network to learn more general features.

5. Residual Blocks: Residual blocks are used in ResNet. They add a shortcut connection that allows the input to skip some layers and be added to the output. This helps gradients flow more easily and makes it possible to train very deep networks.

    The basic idea is:
    Output = F(x) + x

    Here, F(x) is the result of convolution layers, and x is the original input.

    Example: Instead of learning a completely new image feature from zero, a residual block learns only the change needed from the original feature.

6. Depthwise Separable Convolution: Depthwise separable convolution is a lightweight version of normal convolution. It breaks convolution into two steps: first, it applies one filter to each input channel, then it uses a 1 × 1 convolution to combine the channels.

    Example: In a normal convolution, the model learns spatial and channel information together. In depthwise separable convolution, it first finds patterns in each channel separately, then mixes the channels. This reduces computation.

7. MobileNet: MobileNet is a CNN architecture designed for mobile phones and low-power devices. It mainly uses depthwise separable convolutions to reduce the number of parameters and make the model faster.

    Example: A mobile app that detects objects using a phone camera can use MobileNet because it is smaller and faster than large CNN models like VGG or ResNet.

8. Squeeze-and-Excitation Block: A Squeeze-and-Excitation block helps the network decide which channels are important. First, it squeezes each channel into a single value using global average pooling. Then, it learns weights for the channels and increases important channels while reducing less useful ones.

    Example: If a CNN is detecting a bird, some channels may focus on feathers and wings. The SE block can give more importance to those useful channels.

9. Feature Pyramid Network: Feature Pyramid Network, or FPN, is used to detect objects at different sizes. It combines low-level features, which have more detail, with high-level features, which have stronger meaning. This helps the model detect both small and large objects.

    Example:  In a street image, a car may be large and a traffic light may be small. FPN helps the model detect both by using features from different CNN layers.

Simple Summary: 
BatchNorm, LayerNorm, and GroupNorm are normalization methods. Dropout helps prevent overfitting. Residual blocks help train deeper networks. Depthwise separable convolution and MobileNet make CNNs faster and lighter. SE blocks improve channel attention, and FPN improves object detection at multiple scales.

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

### Specialization: Segmentation

**What Is Segmentation?**
- Pixel-level classification vs. bounding-box localization
- Semantic vs. instance vs. panoptic segmentation
- Dense prediction problem framing

**Segmentation Pipeline**
- Encoder (backbone) → decoder (upsampling)
- Skip connections for spatial detail recovery
- Output: per-pixel class map or per-instance mask

**Core Concepts**
- Downsampling/upsampling tradeoff
- Receptive field vs. resolution tension
- Dilated/atrous convolution
- Transposed convolution vs. interpolation upsampling
- Encoder-decoder symmetry

**Semantic Segmentation Architectures**
- FCN: first fully convolutional approach
- U-Net: encoder-decoder, skip connections, medical imaging origin
- DeepLab (v1-v3+): atrous convolution, ASPP, CRF post-processing
- PSPNet: pyramid pooling, global context

**Instance & Panoptic Segmentation**
- Mask R-CNN: RoIAlign, mask head on top of detection
- Panoptic FPN: unifying stuff + things
- YOLACT: real-time instance segmentation
- Panoptic segmentation: stuff (semantic) + things (instance) unified

**Transformer-Era Segmentation**
- SegFormer: lightweight ViT decoder
- Mask2Former: unified mask-classification framing
- Segment Anything (SAM): promptable segmentation, zero-shot masks
- SAM 2: video extension, memory mechanism

**Losses**
- Cross-entropy (per-pixel)
- Dice loss: class imbalance, overlap-based
- Focal loss: hard pixel emphasis
- IoU / Jaccard loss
- Boundary-aware losses

**Segmentation Tricks**
- Class imbalance handling
- Multi-scale inference / test-time augmentation
- CRF refinement
- Auxiliary losses at intermediate layers

**Segmentation Metrics**
- IoU / mIoU
- Pixel accuracy
- Dice coefficient
- Panoptic Quality (PQ)

---

### Specialization: OCR (Optical Character Recognition)

**What Is OCR?**
- Text detection (where) vs. text recognition (what)
- End-to-end OCR vs. two-stage pipelines
- Scene text vs. document text (different difficulty regimes)

**OCR Pipeline**
- Text detection → text recognition → (optional) layout/structure parsing
- Detector localizes text regions/lines/words
- Recognizer transcribes cropped regions into strings

**Text Detection**
- Bounding box vs. polygon/quad detection (curved/rotated text)
- CTPN: sequential text proposals
- EAST: single-shot, rotated boxes
- DBNet: differentiable binarization
- Segmentation-based detection (text as pixel mask)

**Text Recognition**
- CRNN: CNN + RNN + CTC
- CTC loss: alignment-free sequence labeling
- Attention-based recognition (encoder-decoder)
- Transformer-based recognizers (e.g. TrOCR)

**Modern End-to-End & Layout-Aware Models**
- Donut: OCR-free document understanding
- LayoutLM family: text + layout + visual features jointly
- TrOCR: pure Transformer pipeline
- Document VQA framing

**Must-Know Concepts**
- CTC alignment problem
- Beam search decoding
- Character-level vs. word-level vs. subword tokenization
- Handling skew, rotation, curved text
- Multi-language / multi-script challenges

**OCR Tricks**
- Synthetic data generation (SynthText-style)
- Data augmentation for fonts/distortions/backgrounds
- Language model rescoring of outputs
- Post-processing / spell correction

**OCR Metrics**
- Character Error Rate (CER)
- Word Error Rate (WER)
- Detection IoU / F-measure
- Edit distance

---

### Specialization: Vision-Language Models (VLMs)

**What Are VLMs?**
- Joint vision + language representation/generation
- Contrastive alignment vs. generative captioning vs. instruction-following
- Why this builds on CLIP/DINO (Phase 3)

**VLM Pipeline Patterns**
- Vision encoder → projection layer → language model
- Cross-attention fusion vs. early fusion (concatenated tokens)
- Frozen vision encoder + trainable adapter (common pattern)

**Key Architectures & Models**
- CLIP: contrastive image-text pretraining (recap from Phase 3)
- BLIP / BLIP-2: bootstrapped captioning, Q-Former
- Flamingo: few-shot, interleaved image-text
- LLaVA: visual instruction tuning
- GPT-4V / Gemini-style: proprietary multimodal LLMs (architecture at a high level)
- Kosmos: grounding + multimodal generation

**Core Training Concepts**
- Contrastive pretraining (image-text pairs)
- Visual instruction tuning
- Image tokenization strategies (patches, learned queries)
- Alignment vs. generation objectives

**Capabilities & Tasks**
- Zero-shot classification
- Visual question answering (VQA)
- Image captioning
- Visual grounding / referring expressions
- Document/chart understanding

**Must-Know Tradeoffs**
- Hallucination in VLMs
- Resolution vs. compute tradeoffs in vision tokenization
- Catastrophic forgetting when fine-tuning the LM side
- Data quality/scale dependence

**VLM Metrics**
- CIDEr / BLEU / METEOR (captioning)
- VQA accuracy
- Zero-shot top-1 (classification transfer)

---

### Specialization: _Your Track Here_

More specialization tracks are planned. Ideas for future tracks: 3D Vision / Point Clouds • Video Understanding • Generative Models (Diffusion/GANs) • Medical Imaging • Pose Estimation. See the [Contributing](#contributing) section below if you'd like to help add one.

---

## Final Interview Advice

For every topic on this list, push past "I've heard of it" and be able to answer:

- **Why** does this method exist?
- **What** limitation did it solve?
- **What** tradeoff did it introduce?

For each one, aim to know: the **intuition**, the **equations**, the **architecture**, the **tradeoffs**, the **failure cases**, and the **modern successors**.

---

## Contributing

Want to add a specialization track or improve an existing one? See [CONTRIBUTING.md](./CONTRIBUTING.md) for the process.

---

*Found this useful? Star it, fork it, and help make it bigger.*
