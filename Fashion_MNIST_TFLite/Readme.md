# **Running Fashion MNIST Inference on RaspberryPi-3 using  TF-lite**

Fashion MNIST dataset is similar to MNIST data-set which consists of 28x28 greyscale images classified into 10 classes.

More details:https://github.com/zalandoresearch/fashion-mnist

```markdown
### Labels
Each training and test example is assigned to one of the following labels:

| Label | Description |
| --- | --- |
| 0 | T-shirt/top |
| 1 | Trouser |
| 2 | Pullover |
| 3 | Dress |
| 4 | Coat |
| 5 | Sandal |
| 6 | Shirt |
| 7 | Sneaker |
| 8 | Bag |
| 9 | Ankle boot |
```

In this article, we will see how to run a pre-trained neural-network model on Raspberry-Pi 3 model using TFLite framework.

### **Background on TF-Lite**

 **What is TF-lite?**

TfLite is lighter version and next step of TF mobile, which aims to deploy NN models using TF on low-foot print devices like Embedded Systems, Microcontrollers, Mobile, etc.

**What is TFlite Converter?**

TFLite converter uses a pretrained tensorflow model and generates a TFLite model file (.tflite) which is in FlatBuffer format.

More details can be found on official page: https://www.tensorflow.org/lite/convert

In addition to the coversion, TFLite also provides addtional options to optimze while converting into FlatBuffer file format.

**What is need for Quantizing Neural-network models?**

Embedded systems are constrained by memory and processing power. Floating point operation will require additional processing unit (FPU) and will also consume more number of cycles which will turn out to be costlier considering the total number of MACs (Multiplication and Accumlation).

**TFLite Provides below options to optimize models Post-training**

*   Optimize for Size    - tf.lite.Optimize.OPTIMIZE_FOR_SIZE
*   Optimize for Latency - tf.lite.Optimize.OPTIMIZE_FOR_LATENCY
*   Default Optimization - tf.lite.Optimize.DEFAULT


### **Running Inference on RaspberryPi-3**

**Pre-requistes**

Install the following on device:
*   TensorFlow -> Needed for TFlite Converter.
*   tensorflow_datasets -> Needed for using inbuilt datasets of TensorFlow.
*   Numpy -> Needed for image resizing and normalization
*   Matplotlib -> Needed for plotting/saving results.

**Steps to run Inference on Raspberry Pi**
1. Train the model offline using Google Colab (with GPU/TPU)
2. Convert and Save the model to .tflite format using TFLite converter 
3. Import the .tflite model on to the device and run the inference.