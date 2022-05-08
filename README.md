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
The dataset, which contain 1838 images and its label are stored in json file, is provided by Cinnamon AT.
Here is the preview of the raw data
!(raw_data.jpg)
