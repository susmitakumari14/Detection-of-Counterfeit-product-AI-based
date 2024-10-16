# Identifying Counterfeit Products Online, using Image Recognition with MobileNet in Tensorflow

It wasn't too long ago, when counterfeit products were known to be sold out of the back of vans parked next to dingy alleyways. 
However, like most areas of business today, the sale of counterfeit products too has transitioned online following the emergence 
of the digital economy, even making its way to legitimate platforms like Amazon and Ebay.
Most e-commerce websites today are open marketplaces, which means that third-party merchants (or sellers) can list and sell their
products on these platforms. Such a model helps online retailers expand their range of product offerings and attract more shoppers. 
Yet, the same model has unwittingly given room for merchants to sell counterfeits posing as genuine goods.


This is now a **trillion dollar** problem and it not only affects big brands but also plenty of other businesses are seeing their 
revenue, or even entire business, decimated after finding counterfeits of their brands on these online marketplaces.

## Key Characteristics of Online Counterfeit Products:
When I was going through product listings on some major online marketplaces, I realized that there are two main characteristics of any 
online counterfeit product.
1) The sellers use the Brand Logos and Images of the actual product
2) They sell it at a very low price.

![](https://github.com/sheetaldhar/Identifying-Counterfeit-Products-Online-using-Image-Recognition-with-MobileNet-in-Tensorflow/blob/master/Images/Screen%20Shot%202018-08-22%20at%2010.36.29%20AM.png)
## Breaking Down Project Goal into Two Steps:
My goal was to be able automate the process of detecting and identifying these Online Counterfeit listings. This goal had to be 
broken down into two steps. First, I will have to detect these brand logos in images. Second, I would have to find a way to 
classify them as counterfeit vs. genuine

## Step 1: Detecting Brand Logos in Images using Convolutional Neural Nets (MobileNet)
The first step was to be able to detect brand logos in images. For this I prepared a dataset of 10 Brand logos and trained my model to 
detect them in images.To build a logo Detection classifier, I used  MobileNets. **Mobilenets** are a class of small, low latency, low power 
models that can be used for classification , detection and other tasks convolutional neural networks are good for. Since they are really 
small in size, they are considered great deep learning models to be used on mobile devices. For a quick comparison in regrads to size; 
the size of the full VGG60 network on disk is about 553 MB. The size of one the largest mobilenets is about 17 MB. So that’s a huge 
difference, especially when you think about deploying a model to a mobileapp or running it in the browser.It’s architecture is a bit 
different from a traditional CNN in the sense that instead of a single 3x3 convolution layer followed by batch norm and ReLU, MobileNets 
split the convolution into a 3x3 depthwise conv and a 1x1 pointwise conv.
Google open-sourced the MobileNet architecture and released 16 ImageNet checkpoints, each corresponding to a different parameter 
configuration. This gives you an excellent starting point for training your own classifiers that are insanely small and insanely fast.
This paper is great read, if you are interested in knowing more about MobileNets.

<p align="center"> <img width="560" height="400" src="https://github.com/sheetaldhar/Identifying-Counterfeit-Products-Online-using-Image-Recognition-with-MobileNet-in-Tensorflow/blob/master/Images/visual-detection-recognition-and-tracking-with-deep-learning-30-638.jpg">
</p>

After training my model, it was able to detect these 10 brand logos with a high accuracy which made me confident to move to the next step. 
Below you can see the model reaching an accuracy of 100% only after 500 steps. The ROC Curve shows a very low FP rate. 
![](https://github.com/sheetaldhar/Identifying-Counterfeit-Products-Online-using-Image-Recognition-with-MobileNet-in-Tensorflow/blob/master/Images/Screen%20Shot%202018-08-22%20at%203.17.48%20PM.png)

![](https://github.com/sheetaldhar/Identifying-Counterfeit-Products-Online-using-Image-Recognition-with-MobileNet-in-Tensorflow/blob/master/Images/Screen%20Shot%202018-08-14%20at%208.56.59%20PM.png)

### ROC CURVE SHOWING LOW FP RATE

![](https://github.com/sheetaldhar/Identifying-Counterfeit-Products-Online-using-Image-Recognition-with-MobileNet-in-Tensorflow/blob/master/Images/Screen%20Shot%202018-08-20%20at%2012.24.51%20AM.png)

## Step2 : Classifying Counterfeit vs Genuine
Once I had my model give me predictions, it was time for me to work with some real world data and see how can I clasifiy 
a listing into counterfeit vs Genuine. For this I had scareped data of almost 600K product images and their list price from a website 
called ioffer.com. ioffer.com is a website that primarily sells counterfeit products. I wrote a python script that pulls an image and its 
list price from the S3 bucket, sends it to my model and get a prediction. Once I have the prediction, I use a prediction 
threshold, keeping only the ones that are more than 89%. Once I have that, I sent it to the pricing threshold. The pricing threshold 
checks for the list price of the item and if it falls below the set threshold, it is classified as counterfeit. 

![](https://github.com/sheetaldhar/Identifying-Counterfeit-Products-Online-using-Image-Recognition-with-MobileNet-in-Tensorflow/blob/master/Images/Screen%20Shot%202018-08-22%20at%203.18.03%20PM.png)

This will be an effective model if implemented internally within marketplaces, to create an automated system of flagging the postings that
contained counterfeit product listings.

![](https://github.com/sheetaldhar/Identifying-Counterfeit-Products-Online-using-Image-Recognition-with-MobileNet-in-Tensorflow/blob/master/Images/Screen%20Shot%202018-08-22%20at%2012.55.59%20PM.png)



