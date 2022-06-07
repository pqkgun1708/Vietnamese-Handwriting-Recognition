# Vietnamese-Handwriting-Recognition
This is my prethesis project where i attempt to build a model that can take Vietnamese handwritting as image input and process to read them
using CRNN(CNN + RNN) model implemented by Tensorflow 
# Requirement:
* tensorflow, keras
* numpy, pandas
* pickle
* streamlit
# To Do List:
* Clean data
* Read image using openCV
* Preprocess images (resize, grayscale, blur, threshold)
* Split dataset into trainset and testset
* Build CRNN model with CTC loss
* Evaluate
* Calculate metrics for SER, WER and CER
# Data
Data used in this project is provided by Cinnamon AI. It can be downloaded [here](https://drive.google.com/file/d/15ULMGkXxPRadFOqUs1-7BUiZv-_QNpGx/view?usp=sharing)

The dataset have 1838 images and their label are stored in a json file.

Here is the first look of the raw data
![image](https://user-images.githubusercontent.com/52684784/167525733-28edd4a4-1ca5-41b0-99e9-4d1f930661aa.png)
Its label structure in json file
![image](https://user-images.githubusercontent.com/52684784/167524953-3ccafaa4-9468-4f30-954d-e99c28a0939e.png)

Our model
![image](https://user-images.githubusercontent.com/52684784/167296607-7745c197-ee8b-44f8-995c-f5086c813d80.png)

The tradition method of OCR is using CNN where we crop each letter and use them to train our model, however this method have many flaws:
* It cannot predict long sequence text
* Time consuming
* Expensive

In this project, I use the CRNN model which is the combination of CNN, RNN and CTC loss for image-based sequence regconition goal which is perfect in this scenario.
By using CRNN instead of normal CNN, we can shorten the time needed for training and also increase accuracy.
The image will be sliced base on the time step that we define in the RNN step and will be decoded later on using CTC loss function


# Result

By analyzing the loss, i can calculate the most 3 import metrics for text-based regconition task.

![image](https://user-images.githubusercontent.com/52684784/172379339-6e4b0228-1997-4efc-afc9-a445718ecf0d.png)

# UI
I use simple streamlit code to visualize the process for user interaction. It's pretty easy to use, just pick an handwritting image from your computer
and the program will read and print the result on the screen

![image](https://user-images.githubusercontent.com/52684784/172382579-a75027ab-632f-4bb1-b71d-8be7ac4c0f4f.png)


# Ref
These sources are provided by my teacher in this prethesis
* [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
* [CRNN explain](https://www.youtube.com/watch?v=uVbOckyUemo)
* [CTC](https://www.youtube.com/watch?v=eYIL4TMAeRI)
* [Cracking Captcha using only OpenCV and CNN](https://medium.com/@ageitgey/how-to-break-a-captcha-system-in-15-minutes-with-machine-learning-dbebb035a710)
* [Evaluate OCR](https://towardsdatascience.com/evaluating-ocr-output-quality-with-character-error-rate-cer-and-word-error-rate-wer-853175297510)
