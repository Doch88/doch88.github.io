---
layout: post
title:  "Basics of Image Forensics: Compression against AIs"
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
So let's go back to 2007 and talk about compression and **Error Level Analysis (ELA)**.

---

# Compression

Almost every image on the internet is compressed; it would be very expensive to deal with uncompressed images everywhere. <br>
Let's look at an example to understand why. <br>

I took an image with my camera, and I see that it has a resolution of 6000x4000. <br>
Quick math, this means the image has 24.000.000 pixels. Every pixel contains information about the colour, and usually colour in computer science is expressed with 8 bits. <br>
If you know the basics of colour theory, you know that to obtain most colours that exist in this world, you have to mix at least 3 colours - red, green, and blue - which means every pixel carries 8 x 3 bits of information. <br>

So, the weight of this image should be `6000 x 4000 x 8 x 3 = 576.000.000 bits`, corresponding to 72 megabytes. <br>
But, instead, it weighs only 6 megabytes. <br> 
Why? JPEG compression. <br> 

## JPEG Compression and artifacts 

JPEG is the most widely used image compression algorithm. <br>

To make it simple, the algorithm works by removing parts of the image that are barely perceptible to the human eye. It has a parameter, called "quality", that specifies how aggressive the compression should be.
A quality of 100% means that very little information is removed, while 1% means that a lot of the information will be lost. <br>

Since information inside the image will be lost, this means that the content of the image has been altered in some way by the JPEG algorithm. If you were to look at the values of all the pixels inside the image, you would notice that there is a difference. 
Depending on the chosen quality, this difference could be very slight (you wouldn't be able to see it with the naked eye), but it's there, and it's a trace left by our friend JPEG. We call these differences *artifacts*. <br>

Now the interesting part comes. <br> 
Since our JPEG compression was applied to the whole image, these artifacts should always be **consistent** inside the image. 
If the image was tampered with in some way - let's say by removing something with Photoshop, for example - this will affect the JPEG artifacts as well.
You would notice an inconsistency of these artifacts in the particular area of the image that was altered. <br>
And this is exactly what ELA is based on.

---

# Error Level Analysis

It was 2007 when [Dr. Neal Krawetz](https://www.hackerfactor.com/) introduced, among other algorithms, ELA in his presentation called [A Picture's Worth...](https://www.blackhat.com/html/bh-usa-07/bh-usa-07-speakers.html#Krawetz). <br>
The idea is simple: 

 - We have the image we want to analyse
 - We compress it with JPEG, with a chosen quality factor - this will become a parameter of ELA.
 - We calculate the difference between the two images.
   
The result would be an ELA map that we will have to interpret. <br> 
Of course, the main assumption of ELA is that the image (or part of the image) was compressed with JPEG at some point. <br>

Let's use a toy example to explain how it works. <br>

## Toy example

Using something from my domain of work, let's consider this specimen of a French national ID card. <br>

![French specimen](/assets/images/ela/original.jpg)

In this toy example, let's assume I know that it was compressed using JPEG with a quality of 95%. I will use this information later. <br>
Now, I inpaint the image with an AI model, and I get this:

![Deepfake](/assets/images/ela/deepfake.png)

And, very important, I **save this deepfake in a PNG format**. <br>
PNG, unlike JPEG, uses a *lossless* compression algorithm, which means information will not be lost when compressing the image. <br>

Now, using the information from before, we will perform ELA with a **JPEG quality of 95%**.

| ![French specimen](/assets/images/ela/original.jpg)  | ![ELA French specimen](/assets/images/ela/ela_original.jpg)  |
|---|---|
| ![Deepfake](/assets/images/ela/deepfake.png)  | ![French specimen](/assets/images/ela/ela_deepfake.jpg)  |

The area that was tampered with is super evident. We successfully detected our deepfaked ID document and avoided a fraudster. <br>

But in reality, it's very unlikely that you will know the initial JPEG quality factor (especially if the image was altered), and it would be super lucky if, on top of that, the altered image was saved as a PNG.

## Real example

Let's assume that our deepfake was saved as a JPEG instead. <br>
We know nothing about quality factors; we only know that, if the image was altered, then there should be some inconsistency on the ELA map caused by one part of the image being double compressed and the deepfaked part being compressed only once.

We will perform ELA with a JPEG quality of 80% for both images, in this case.

| ![French specimen](/assets/images/ela/original.jpg)  | ![ELA French specimen](/assets/images/ela/ela_original_80.jpg)  |
|---|---|
| ![Deepfake](/assets/images/ela/deepfake.png)  | ![French specimen](/assets/images/ela/ela_deepfake_80.jpg)  |

As you can see now, this is where ELA becomes more like an art. <br>
There is clearly a difference, but without knowing that the image was tampered with, would it be possible to understand from the ELA map? <br>
Maybe yes, with some experience, but it's still a very error-prone technique. The first thing that has to be taken into consideration comes from how JPEG works. <br>

In short, some notes:
- JPEG will create a lot more artifacts with high contrast areas, such as text or borders, and this will result in a brighter ELA.
- Flat surfaces should have the same ELA values.
- Similar texture also means similar ELA.

If some part of the image doesn't respect these 'rules', then it might be suspicious. Like the deepfaked face on the ID, which has a suspiciously bright ELA. <br>
For other tips, I suggest referring to [FotoForensics](https://fotoforensics.com) and their tutorials.

---

# Conclusions

So, can ELA be a solution to detect AI-manipulated images? <br>
No, not by itself anyway. <br>

ELA is just a tool in the Image Forensics toolbox that can help fight deepfakes. <br>
But many other things can be used together with ELA, such as EXIF information, PRNU, PCA and so on. And probably some of these techniques will be the topic for another post.



