---
layout: post
title:  "Basics of Image Forensics: Noise against AIs"
date:   2025-09-15 20:15:09 +0200
tags: ai tech image forensics 
---

Let's start with some context. Why am I writing this post?

I work at [Fourthline](https://www.fourthline.com/), a company that manages the Know Your Customer (KYC) process of companies like Revolut, TradeRepublic, and N26. <br>
For those who don't know what KYC is, think of when you have to register online to use the services provided by one of these companies, and you have to take a selfie and a picture of your ID document to show you are who you claim you are. <br>
That's KYC in a nutshell, and as you may understand, we don't want to let fraudsters in. If you ever played [Papers, Please](https://en.wikipedia.org/wiki/Papers,_Please), you can imagine that sometimes this is not super easy. <br>

Fraudsters are getting better and better, and technology is significantly aiding them. <br>
Deepfakes and AI-generated selfies and documents are becoming one of their tools, and my job at Fourthline is also to fight this kind of AI. <br>
Yes, I'm an AI engineer who fights AI. A cyberwar that is destined to become even more difficult as technology advances. <br>

But in order to fight deepfakes, I should study and understand how similar problems were dealt with in the past. <br>
In the end, image manipulation was a thing even 15 years ago, when generative models weren't as good as now. <br>
So let's go back to 2007 and talk about Error Level Analysis (ELA).

# JPEG Artifacts 

Every image 
Let's take an image of resolution 1980x1024. <br>
Quick math, this means we have 2.073.600 pixels. Every pixel contains information about the colour, and usually colour in computer science is expressed with 8 bits. <br>
Common images are in the RGB format, which means that every pixel has information about the quantity of red, green and blue that are mixed together to obtain a specific colour. <br>
So, a
