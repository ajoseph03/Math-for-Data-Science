# PyTorch AlexNet Model Setup

This simple setup guide explains how to load label mappings from a JSON file and initialize a pretrained AlexNet model using PyTorch for image classification tasks.

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Usage](#usage)

## Introduction

The given code snippet is part of a larger pipeline for image classification using the AlexNet model, a popular deep learning model in PyTorch. The code covers two primary aspects:
- Loading label mappings from a remote JSON file.
- Initializing and setting up the AlexNet model in evaluation mode.

## Prerequisites

Before proceeding, ensure you have the following:
- Python installed on your system.
- PyTorch library installed. You can find installation instructions on the [PyTorch official website](https://pytorch.org/get-started/locally/).
- An environment that supports CUDA for GPU acceleration (optional but recommended for faster processing).

## Installation

(Instructions on how to install and setup any additional dependencies or setup steps needed for your project)

## Usage

### Loading Label Mappings

The code starts by loading label mappings from a remote JSON file hosted on AWS S3. These labels are likely to correspond to the classes recognized by the AlexNet model.

```python
import requests

labels = {int(key):value for (key, value) in requests.get('https://s3.amazonaws.com/mlpipes/pytorch-quick-start/labels.json').json().items()}
```

### Initializing AlexNet Model

The AlexNet model, a well-known architecture in deep learning for image classification, is then loaded with pretrained weights. The model is transferred to the GPU if available and set in evaluation mode.

```python
import torch
from torchvision.models import alexnet

device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")
model = alexnet(pretrained=True).to(device)
model.eval()
```

The `model.eval()` call is crucial as it sets the model to evaluation mode, affecting layers like dropout and batch normalization which behave differently during training.

---
