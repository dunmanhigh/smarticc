---
title: Detecting SMS scams with AI
categories: article
tags: project AI
author: Poh Say Keong
image: "/assets/img/2019-05-20-detecting-sms-scams-preview.png"
---

## Introduction
The Scam Text Checker is a webapp dedicated to detecting malicious texts targeted at the elderly and older support staff. On the backend, the app makes use of machine learning to detect potential malicious messages from a trained dataset. On the frontend, a simple and intuitive interface is used so that it is easier for the elderly to navigate.


## Why is this app important?
There have been a rise of loan scams targeting the elderly in recent years. In 2018, elderly persons were cheated of $88,000 in loan sums between January and September, a huge jump from the $4,700 that seniors lost to such scam in 2017. Loan scam victims typically receive SMS or WhatsApp messages offering loan services and then receive instructions to transfer money as a deposit before the loan can be disbursed. The police have launched an anti-scamming programme for seniors amid this rise in loan scams. Our app intends to act as a supporting tool to elderly to make it easier for them to protect themselves from such scams. 


## Where to find our app?
Our app can be found at this [link](http://bit.ly/smsscam)  
  
![][image-1]

![][image-2]

These are screenshots of our app running on mobile devices. A red box indicates that the text is likely to be scam while a green box indicates that the text is likely to be harmless. Feel free to test out our app by entering some of the suspicious messages that you have received!


## What goes behind the app?
We made use of fastText, an open-source library that allows the machine to learn text representations and text classifiers. We trained our model with The National University of Singapore SMS Corpus which is a collection of 67,093 SMS messages mostly from Singaporeans and mostly from NUS students.

The computer is able to convert each individual word and punctuation into numbers that collectively indicate how likely an entry is a scam. This technique is a component of Natural Language Processing (NLP) that aims to to program computers to process and analyze large amounts of natural language data.

A good starting point to learn more about NLP can be [Natural Language Toolkit(NLTK)](https://www.nltk.org/). It makes use of a language that many of us are familiar with (Python) and there are many good tutorials out there to get you started.

[image-1]: {{ "/assets/img/2019-05-20-detecting-sms-scams-1.png" | absolute_url }}
[image-2]: {{ "/assets/img/2019-05-20-detecting-sms-scams-2.png" | absolute_url }}
