# NLP-Prjects

## Email Spam Detection Using BERT in Tensorflow and Keras
#### Using BERT and Tensorflow 2.0, we will write simple code to classify emails as spam or not spam. BERT will be used to generate sentence encoding for all emails and after that we will use a simple neural network with one drop out layer and one output layer. 

### The Pipeline Overview for Spam Detection Using BERT
#### To build the system ourselves we are going to follow these procedures:

#### 1. Load Data – We will be loading our data which is simple [2 categories(ham and spam) along with corresponding emails] CSV file. The file can be found here "https://www.kaggle.com/venky73/spam-mails-dataset"

#### 2. EDA – Perform some EDA to get a feel of what data looks like

#### 3. Pre Processing – Based on the results of EDA we will be going to apply some preprocessing to the data to make it model friendly

#### 4 – Model Creation – We will use Functional API* to build our Deep Learning Model which will consist of

#### INPUT – Will create an input layer that will take in all the pre-processing data and pass it to bert_processor.
#### BERT PREPROCESSOR – Process our input text to be in the format which encoder accepts. (adds MASK AND ENCODINGS).
#### BERT ENCODER – Feed our processed text to the bert model which will eventually generate a contextualized word embedding for our training data.
#### DROPOUT – Add a dropout layer that will randomly drop out a few neurons from the network to take care overfitting problem.
#### Sigmoid – At last we will add a softmax layer to predict data in 2 categories.
#### 5- Model Evaluation – Further we will check how the model performs on the test data and plot some relevant charts and metrics based on the observations.
#### 6- Predict Data – Finally we will predict our own emails using the model.

#### Here is a general visualization of the flow of logic:



## This article was published as a part of the Data Science Blogathon

Introduction
In the previous article, we have talked about BERT, Its Usage, And Understood some of its underlying Concepts. This article is intended to show how one can implement the learned concept to create a spam classifier using BERT.

Table Of Contents
Introduction
Understanding Spam Emails
Overview Of The Pipeline
Implementing Spam Detection
Understanding Spam Emails
Let’s suppose you got up in the morning and opened your Gmail and found a mail saying something like:

“Hey, you have won an iPhone 10 in the luck draw conducted by amazon yesterday. To receive the prize please log in to your account and claim your gift.”

Seeing mail you first checked the sender and you found him to be genuine, and you happily rushed to the site and logged in and found there was no prize at all. Feeling sad you returned to your works.

A few hours later you received a message stating there has been a recent transaction from your bank account and you are shocked how it happened. After telling the incident to the bank, they told you have been spammed and millions are facing the same difficulty, sounds terrible right!

But my friends luckily for you google has some type of mechanism to find these emails and separate them in its SPAM folder(see fig 1.1).

spam folder | Spam Detection Using BERT
Spam Folder: – Image By Author
Spam emails are unwanted emails share in bulk intending to gather data/ do phishing/ perform social engineering/ start an attack and a lot more – mostly for bad causes. Usually, these are in form of advertisement and marketing stuff.

Since these are sent in bulk, each one will have a similar underlying pattern and format, so what the mechanism of google does is finds these underlying patterns and separates them.

This method is generally called spam classification and uses a model which is trained on spam and not a spam set of data.

The Pipeline Overview for Spam Detection Using BERT
To build the system ourselves we are going to follow these procedures:

1. Load Data – We will be loading our data which is simple [2 categories(ham and spam) along with corresponding emails] CSV file. The file can be found here

2. EDA – Perform some EDA to get a feel of what data looks like – statistics here!

3. Pre Processing – Based on the results of EDA we will be going to apply some preprocessing to the data to make it model friendly

4 – Model Creation – We will use Functional API* to build our Deep Learning Model which will consist of

INPUT – Will create an input layer that will take in all the pre-processing data and pass it to bert_processor.
BERT PREPROCESSOR – Process our input text to be in the format which encoder accepts. (adds MASK AND ENCODINGS).
BERT ENCODER – Feed our processed text to the bert model which will eventually generate a contextualized word embedding for our training data.
DROPOUT – Add a dropout layer that will randomly drop out a few neurons from the network to take care overfitting problem.
SOFTMAX – At last we will add a softmax layer to predict data in 2 categories.
+ 2 more generic steps.
5- Model Evaluation – Further we will check how the model performs on the test data and plot some relevant charts and metrics based on the observations.

6- Predict Data – Finally we will predict our own emails using the model.

Here is a general visualization of the flow of logic:

Logical flow | Spam Detection Using BERT
 Image By Author
Functional API

A way to create models with more flexibility and complexity than traditional sequential models. Complexity includes- Shared layers, Multiple Inputs – Outputs, and much more.

Here is how one can quickly create a model using functional API:

Layer1 = Input(shape = (shape),  name = 'layer_name')
Dense = Dense(num_units = units, activation = activation, name = 'dense')(Layer1)
model = Model(inputs = [Layer1], outputs = [Dense])
So all you have to do is pass the last previous layer as an input to the current layer and finally call the create the model using Model(inputs, outputs).

Implementing Spam Detection Using BERT
To start we will first download a readily available dataset which can be downloaded from the link given earlier. Once you downloaded it will look something like this:

The spam detection dataset
 Image By Author
Here ham – Good Mails and Spam – Spam mails. Our job will be to build a model which can train on the data and return prediction when given new inputs.

Loading Dependencies
