# Image_Super_Resolution_Using_DNNs_SoC

## Abstract
In this project we employ an Efficient Sub-Pixel Convolutional Neural Network (ESPCN) for real-time single image and video super-resolution. The recovery of a high resolution (HR) image or video
from its low resolution (LR) counter part is topic of great interest in digital image processing. This task is referred to as super-resolution and finds great applications in medical imaging, satellite imaging, face recognition and surveillance.

---

## Implementation
This is an attempt to implement the [research paper](https://github.com/Vishal-Bysani/Image_Super_Resolution_Using_DNNs_SoC/blob/main/Papers/160905158v2.pdf) on ESPCN. The task of this model is to estimate the super-resolved image ($I^{SR}$), given a low-resolution image($I^{LR}$) downsampled from the high-resolution image ($I^{HR}$). The downsampling operation is known: to produce $I^{LR}$ from $I^{HR}$ by convolving with a Gaussian filter and then downsampling it by factor r(upscaling ratio).<br>

To recover $I^{SR}$, a 3 layer convolutional network is used. In our architecture, we first apply a 2 layer convolutional neural network directly to the LR image, and then apply a sub-pixel convolution layer that upscales the LR feature maps to produce $I^{SR}$.

For the ESPCN, we set (f1 , n1 ) = (5, 64), (f2 , n2 ) = (3, 32) and f3 = 3 in our evaluations. In the training phase, 17r x 17r pixel sub-images are extracted from the training ground truth images $I^{HR}$ , where r is the upscaling factor. To synthesize the low-resolution samples $I^{LR}$ , we blur $I^{HR}$ using a Gaussian filter and sub-sample it by the upscaling factor. The sub-images are extracted from original images with a stride of (17-&Sigma;mod (f, 2)) x r from $I^{HR}$ and a stride of 17-&Sigma;mod (f, 2) from ILR . This ensures that all pixels in the original image appear once and only once as the ground truth of the training data. The activation function used in the model is tanh function.

## Setup
Please setup your training environemnt by installing the requirements using:

```
$ pip install -r requirements.txt
```

## Training
To run the model training, use the following command:

```
$ python3 train.py -t ./dataset/train -v ./dataset/val -o ./assets/models/
```

This will train the model and save the model's weights as `state_dict()` to the `assets/models/` folder.

## Testing
To test the model, use the following command:

```
$ python3 infer.py -w ./assets/models/best.pth -i ./dataset/test/monarch.png -o ./assets/dataset/outputs
```









