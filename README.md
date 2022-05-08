# Vietnamese-Handwriting-Recognition
This is my prethesis project where i use what i learn to make a model that can read Vietnamese handwritten as image input and process to read them
using CRNN(CNN + RNN) model implemented by Tensorflow 
# Here's what im gonna do:
* Find all widths and heights of images
* Use openCV to read image
* Preprocess images (like converting images to greyscale)
* Resize images so all images will have the same size
* Split your dataset into trainset and testset
* Build CRNN model with CTC loss
* Prediction
* Calculate metrics for SER, WER and CER
# Data preprocessing
The dataset include 1838 images and its label are stored in json file, which is provided by Cinnamon AI.
Here is thefirst look of the raw data
![](raw_data.jpg)
Its label structure in json file
![](label.png)
Our pipeline
![image](https://user-images.githubusercontent.com/52684784/167296607-7745c197-ee8b-44f8-995c-f5086c813d80.png)
The tradition method of OCR is using CNN where we crop each leter and use them to train our model, however this method have many flaws:
* It cannot predict long sequence text
* Time consuming
* Expensive

In this project, I use the CRNN model which is the combination of CNN, RNN and CTC loss for image-based sequence regconition goal which is perfect in this scenario.
By using CRNN instead of normal CNN, we can shorten the time needed for training and also increase accuracy.
The image will be sliced base on the time step that we define in the RNN step and will be decoded later on using CTC loss function
![image](https://user-images.githubusercontent.com/52684784/167296961-bf4692bf-77ba-48a3-a129-44904168750a.png)

This is my model summary.
__________________________________________________________________________________________________
Layer (type)                    Output Shape         Param #     Connected to                     
==================================================================================================
input_1 (InputLayer)            [(None, 118, 2167, 1 0                                            
__________________________________________________________________________________________________
conv2d (Conv2D)                 (None, 118, 2167, 64 640         input_1[0][0]                    
__________________________________________________________________________________________________
max_pooling2d (MaxPooling2D)    (None, 39, 722, 64)  0           conv2d[0][0]                     
__________________________________________________________________________________________________
activation (Activation)         (None, 39, 722, 64)  0           max_pooling2d[0][0]              
__________________________________________________________________________________________________
conv2d_1 (Conv2D)               (None, 39, 722, 128) 73856       activation[0][0]                 
__________________________________________________________________________________________________
max_pooling2d_1 (MaxPooling2D)  (None, 13, 240, 128) 0           conv2d_1[0][0]                   
__________________________________________________________________________________________________
activation_1 (Activation)       (None, 13, 240, 128) 0           max_pooling2d_1[0][0]            
__________________________________________________________________________________________________
conv2d_2 (Conv2D)               (None, 13, 240, 256) 295168      activation_1[0][0]               
__________________________________________________________________________________________________
batch_normalization (BatchNorma (None, 13, 240, 256) 1024        conv2d_2[0][0]                   
__________________________________________________________________________________________________
activation_2 (Activation)       (None, 13, 240, 256) 0           batch_normalization[0][0]        
__________________________________________________________________________________________________
conv2d_3 (Conv2D)               (None, 13, 240, 256) 590080      activation_2[0][0]               
__________________________________________________________________________________________________
batch_normalization_1 (BatchNor (None, 13, 240, 256) 1024        conv2d_3[0][0]                   
__________________________________________________________________________________________________
add (Add)                       (None, 13, 240, 256) 0           batch_normalization_1[0][0]      
                                                                 activation_2[0][0]               
__________________________________________________________________________________________________
activation_3 (Activation)       (None, 13, 240, 256) 0           add[0][0]                        
__________________________________________________________________________________________________
conv2d_4 (Conv2D)               (None, 13, 240, 512) 1180160     activation_3[0][0]               
__________________________________________________________________________________________________
batch_normalization_2 (BatchNor (None, 13, 240, 512) 2048        conv2d_4[0][0]                   
__________________________________________________________________________________________________
activation_4 (Activation)       (None, 13, 240, 512) 0           batch_normalization_2[0][0]      
__________________________________________________________________________________________________
conv2d_5 (Conv2D)               (None, 13, 240, 512) 2359808     activation_4[0][0]               
__________________________________________________________________________________________________
batch_normalization_3 (BatchNor (None, 13, 240, 512) 2048        conv2d_5[0][0]                   
__________________________________________________________________________________________________
add_1 (Add)                     (None, 13, 240, 512) 0           batch_normalization_3[0][0]      
                                                                 activation_4[0][0]               
__________________________________________________________________________________________________
activation_5 (Activation)       (None, 13, 240, 512) 0           add_1[0][0]                      
__________________________________________________________________________________________________
conv2d_6 (Conv2D)               (None, 13, 240, 1024 4719616     activation_5[0][0]               
__________________________________________________________________________________________________
batch_normalization_4 (BatchNor (None, 13, 240, 1024 4096        conv2d_6[0][0]                   
__________________________________________________________________________________________________
max_pooling2d_2 (MaxPooling2D)  (None, 4, 240, 1024) 0           batch_normalization_4[0][0]      
__________________________________________________________________________________________________
activation_6 (Activation)       (None, 4, 240, 1024) 0           max_pooling2d_2[0][0]            
__________________________________________________________________________________________________
max_pooling2d_3 (MaxPooling2D)  (None, 1, 240, 1024) 0           activation_6[0][0]               
__________________________________________________________________________________________________
lambda (Lambda)                 (None, 240, 1024)    0           max_pooling2d_3[0][0]            
__________________________________________________________________________________________________
bidirectional (Bidirectional)   (None, 240, 1024)    6295552     lambda[0][0]                     
__________________________________________________________________________________________________
bidirectional_1 (Bidirectional) (None, 240, 1024)    6295552     bidirectional[0][0]              
__________________________________________________________________________________________________
dense (Dense)                   (None, 240, 141)     144525      bidirectional_1[0][0]            
__________________________________________________________________________________________________
the_labels (InputLayer)         [(None, 240)]        0                                            
__________________________________________________________________________________________________
input_length (InputLayer)       [(None, 1)]          0                                            
__________________________________________________________________________________________________
label_length (InputLayer)       [(None, 1)]          0                                            
__________________________________________________________________________________________________
ctc (Lambda)                    (None, 1)            0           dense[0][0]                      
                                                                 the_labels[0][0]                 
                                                                 input_length[0][0]               
                                                                 label_length[0][0]               
==================================================================================================
Total params: 21,965,197
Trainable params: 21,960,077
Non-trainable params: 5,120
__________________________________________________________________________________________________


