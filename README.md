# Vietnamese-Handwriting-Recognition
This is my prethesis project where i use what i learn to make a model that can take Vietnamese handwritten as image input and process to read them
using CRNN(CNN + RNN) model implemented by Tensorflow 
# Here's what im gonna do:
* Find all images width, height
* Read image using openCV
* Preprocess images (resize, grayscale, blur, threshold)
* Split dataset into trainset and testset
* Build CRNN model with CTC loss
* Prediction
* Calculate metrics for SER, WER and CER
# Data preprocessing
Data used in this code are downdload [here](https://drive.google.com/file/d/15ULMGkXxPRadFOqUs1-7BUiZv-_QNpGx/view?usp=sharing)

The dataset include 1838 images and its label are stored in json file, which is provided by Cinnamon AI.

Here is the first look of the raw data
![](raw_data.jpg)
Its label structure in json file
![](label.png)

Our model
![image](https://user-images.githubusercontent.com/52684784/167296607-7745c197-ee8b-44f8-995c-f5086c813d80.png)

The tradition method of OCR is using CNN where we crop each letter and use them to train our model, however this method have many flaws:
* It cannot predict long sequence text
* Time consuming
* Expensive

In this project, I use the CRNN model which is the combination of CNN, RNN and CTC loss for image-based sequence regconition goal which is perfect in this scenario.
By using CRNN instead of normal CNN, we can shorten the time needed for training and also increase accuracy.
The image will be sliced base on the time step that we define in the RNN step and will be decoded later on using CTC loss function
![image](https://user-images.githubusercontent.com/52684784/167296961-bf4692bf-77ba-48a3-a129-44904168750a.png)

# Result
The training process took me around 

By analyzing the loss, i can calculate the most 3 import metrics for text-based regconition task
* CER (Character error rate): 
* WER (Word error rate):
* SER (Sequence error rate): 

# Ref
These sources are provided by my supervisor teacher in this prethesis
* [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
* [CRNN explain](https://www.youtube.com/watch?v=uVbOckyUemo)
* [CTC](https://www.youtube.com/watch?v=UMxvZ9qHwJs)
* [Cracking Captcha using only OpenCV and CNN](https://medium.com/@ageitgey/how-to-break-a-captcha-system-in-15-minutes-with-machine-learning-dbebb035a710)
* [Evaluate OCR](https://towardsdatascience.com/evaluating-ocr-output-quality-with-character-error-rate-cer-and-word-error-rate-wer-853175297510)
* [Nhận diện text trong hình ảnh với CRNN+CTC](https://viblo.asia/p/nhan-dien-text-trong-hinh-anh-voi-crnnctc-Eb85o9rBZ2G)
