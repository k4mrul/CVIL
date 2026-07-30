
A Convolutional Neural Network (CNN) is a neural network commonly used for image processing. It learns to recognize patterns such as edges, shapes, textures, and objects.

## Convolution

Convolution is the process of moving a small filter across an image. At each position, the filter performs a calculation to find a particular pattern.

Example: A convolution may find the edges of a person’s face in a photograph.

## Kernels

A kernel, also called a filter, is a small grid of numbers used during convolution. Different kernels detect different features.

Example: One kernel may detect horizontal lines, while another may detect vertical lines.

## Receptive Fields

The receptive field is the area of the input image that influences a particular neuron.

In early CNN layers, a neuron may see only a small area. In deeper layers, it can indirectly see a much larger part of the image.

Example: An early neuron may detect a small edge, while a deeper neuron may recognize an entire eye or face.

## Padding

Padding adds extra pixels (usually zero) around an image before convolution. It helps preserve the image size and keeps information near the borders.

Example: Zero padding surrounds an image with pixels whose values are zero.

## Stride

Stride is the number of pixels a kernel moves at each step. A larger stride creates a smaller output.

Example: A stride of 1 moves one pixel at a time, while a stride of 2 moves two pixels at a time.

## Dilation

Dilation adds spaces between the elements of a kernel. This allows the kernel to examine a larger area without adding more values.

Example: A dilated kernel can detect a large object pattern while using a small 3 × 3 kernel.

## Pooling

Pooling reduces the size of a feature map (feature map shows where and how strongly a feature was detected). It keeps important information while reducing computation.

Example: Max pooling selects the largest value from a small area. From the values 1, 3, 2, 4, it selects 4.

## Feature Hierarchies

CNN layers learn features in increasing levels of complexity. Early layers detect simple patterns, while deeper layers detect complete objects.

Example: A CNN may learn edges first, then eyes and ears, and finally recognize a cat.

## Translation Invariance

Translation invariance means that a CNN can recognize an object even when its position changes in the image. Because the same kernel is applied across all spatial locations, a pattern learned in one corner of training images will be detected equally well in the center of test images.

Example: A CNN can recognize a car whether it appears on the left, in the center, or on the right side of an image.
