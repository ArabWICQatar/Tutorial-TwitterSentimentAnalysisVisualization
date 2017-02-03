# **Twitter Sentiment analysis & Visualization**

## Introduction

### Objective

Perform Sentiment analysis and visualization on tweets to compare and contrast events or topics on Twitter. Analyzing the sentiment of three popular Airlines of Middle East: Qatar Airways, Emirates and Etihad is the objective of this project.

### **Purpose & Overview**

This tutorial is a Do It Yourself project, organised as a part of the Women in Data Science Qatar event. The tutorial is self paced with sufficient explanations and further references under each module. Code for the project can also be found in the [github repository](https://github.com/ArabWICQatar/TwitterSentimentAnalysisVisualization).

This project will concentrate on Sentiment Analysis and Visualization of Twitter data. Various modules such as: data collection from Twitter, pre-processing, sentiment analysis and visualization are involved.

### **Requirements**

Python 2.7

Python modules: Tweepy & TextBlob

### **Installation**

**INSTALLING PYTHON:**

For Windows, go to[https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)and click onDownload and install Python 2.7.13, the latest version.Be sure to check on add path to environment variable while installing.

For Mac OSx, got to[https://www.python.org/downloads/mac-osx/](https://www.python.org/downloads/mac-osx/)scroll and download thePython 2.7.13, latest version.

For Linux, Ubuntu, download and install the python2.x package from[https://www.python.org/downloads/source/](https://www.python.org/downloads/source/).

![](https://lh5.googleusercontent.com/9HmanYIO54GaBn9H8miTWI_vDQ-xmjkUrWbgZntYmvr7wdF85sV3vmxq8-qPWwsuqsd9G7qiI36688AanC3cvem1AExsXk7UEzXeKiME9iWUb168c5DZrTGVNoSyETWcZqWBmu7L)

On installing Python 2.7, to test if it’s installed properly, open command prompt or terminal and type `python`

You will get a similar response depending on your OS:

> `Python 2.7.11 (v2.7.11:6d1b6a68f775, Dec 5 2015, 20:32:19) [MSC v.1500 32 bit (Intel)] on win32`
>
> `Type "help", "copyright", "credits" or "license" for more information.`

#### **INSTALLING PYTHON LIBRARIES:**

On installing python, type the following commands from the command prompt or terminal.

We will first download the python package installer PyPA to install python libraries. To install pip installer, follow the instructions below.

**For Windows:**

Search for command prompt desktop app

Right click and run command prompt as administrator

Type the following in command prompt: \(note that -U will install all dependencies required for any package/ library\)

`python -m pip install -U pip`

**For Mac:**

To open Terminal go to : Application/utility/Terminal

Then write the following command on the terminal:\(Type sudo at the beginning of admin privileges are required\)

`pip install -U pip`

**For Linux:**

Open Terminal and type the following command. \(Type sudo at the beginning of admin privileges are required\)

`pip install -U pip`

Now the tweepy and textblob python modules are downloaded, we will use tweepy for authenticating and connecting with Twitter, to collect tweets and TextBlob for performing sentiment analysis. TextBlob is used for many other NLP use-cases such as parts-of-speech tagging, one of the popular usage is sentiment analysis.

Type the following commands one after the other, in your command prompt or terminal to install the python libraries.

Tweepy :-  `pip install -U tweepy`

TextBlob :-  `pip install -U textblob`

NOTE: For programming using python, you can use the Python IDLE installed in your system to edit and run your code. Or use any text editor of your choice to edit and run your code using command prompt from the specific folder where your project is located.

_You are now ready to do Twitter Sentiment Analysis and Visualization! Get started with the _[_Data Collection from Twitter_](/chapter1.md)_._

