# Lab-3.2---CNN-Architectures-LeNet-VGG-ResNet
This README explores the evolution of Convolutional Neural Network architectures, comparing the custom **LeNet-style** approach with industry-standard models like **VGG** and **ResNet**. 

---


In this lab, we transition from building basic models to using sophisticated, pre-defined architectures. We explore how increasing depth and changing connectivity (like skip connections) allows models to solve more complex visual problems like CIFAR-10.

## 🏛️ Architecture Comparison

### 1. LeNet (SimpleCNN)
A classic, lightweight architecture designed for grayscale digit/clothing recognition.
* **Structure:** Two sets of Conv-ReLU-MaxPool layers followed by fully connected layers.
* **Pros:** Very few parameters; extremely fast to train on simple datasets.


### 2. VGG (Visual Geometry Group)
VGG introduced the idea of using very small ($3 \times 3$) filters but stacking many of them to create a deep network.
* **Key Feature:** Uniformity. It uses the same kernel size and max-pooling settings throughout.
* **Cons:** Extremely high parameter count (especially in the final linear layers), making it memory-intensive.


### 3. ResNet (Residual Network)
The breakthrough that allowed networks to become hundreds of layers deep without the gradients "vanishing."
* **Residual Learning:** It uses **Skip Connections** (Identity Shortcuts) that allow the gradient to flow through the network more easily by bypassing one or more layers.
* **Efficiency:** Despite being much deeper than VGG, ResNet-18 is significantly more efficient in terms of parameter count.


---

## 🛠️ Key Implementation Tasks

### 🔧 Adapting Pretrained Models
Standard models like VGG and ResNet are typically built for **ImageNet** ($3$ RGB channels, $224 \times 224$ resolution). In this lab, we demonstrate how to modify these "off-the-shelf" models:
* **Input Layer:** We manually adjust `vgg.features[0]` and `resnet.conv1` to accept $1$-channel (Grayscale) FashionMNIST images.
* **Output Layer:** We set `num_classes=10` to match the categories in FashionMNIST or CIFAR-10.

### 🖼️ Training on CIFAR-10
Unlike the $28 \times 28$ FashionMNIST images, CIFAR-10 contains $32 \times 32$ color images of objects (planes, cars, birds, etc.). 
* **Scaling:** We use `transforms.Resize(224)` to upscale CIFAR images so they are compatible with the default ResNet architecture.
* **Normalization:** We apply specific mean and standard deviation values calculated from the CIFAR-10 dataset to help the model converge faster.

---

## 📊 Summary of Results

| Model | Parameters (Approx) | Best Use Case |
| :--- | :--- | :--- |
| **SimpleCNN** | ~400k | Small grayscale datasets (MNIST) |
| **ResNet-18** | ~11M | Real-world images, complex object detection |
| **VGG-11** | ~128M | Legacy applications, high-power compute |

---

## 🚀 How to Use
1.  **Inspect Parameters:** Run the script to see the massive difference in parameter counts between the three models.
2.  **CIFAR-10 Training:** The script will download CIFAR-10 and begin training a ResNet-18. 
3.  **Performance:** Observe how a deep architecture like ResNet handles "real-world" objects compared to the simpler models used in previous labs.

> **Expert Tip:** Notice that while VGG is much larger than ResNet-18, ResNet often achieves higher accuracy. This demonstrates that **architectural design** (like skip connections) is often more important than just "adding more neurons."
