---
layout: post
title:  "AI Engineers aren’t safe from being replaced by AI"
date:   2025-08-17 17:32:31 +0200
tags: ai random
---
It quickly became small talk; whenever I speak with a fellow engineer working in tech, we somehow always end up in the same direction:

> “AI agents are getting so smart nowadays, my job will eventually be replaced by them. You don’t have to worry about this instead. You are an AI engineer, you create AIs, you cannot be replaced.”


My face takes a specific expression at this point, showing some sort of discomfort, mixed with a “how do I explain this now in simple terms?” kind of face. The kind of face you have when you meet a stranger in the elevator and you don’t know how to act.

The fact is, it will be very likely that my job will be replaced sooner than most developer jobs.

Let’s dive into the reasons why I think this, starting by defining what an AI engineer is.

---


## What exactly is an AI engineer?

The idea for this post came after seeing this image on my LinkedIn feed:

![Book page](/assets/images/1_tXcgmhR3NbSYRefglt9g_A.jpeg)

This excerpt was posted by Arvind Narayanan, and it comes from his book “AI Snake Oil: What Artificial Intelligence Can Do, What It Can’t, and How to Tell the Difference”, written together with Sayash Kapoor.[^1]

Although I didn’t read the book myself, I think this introduction explains the current situation with AI — and AI engineers — very well. At this moment in the world, artificial intelligence is everything and nothing at the same time.  
ChatGPT is AI, the software that post-processes images on your camera phone is AI, the algorithm that selects the best commercials to show you on social media is AI, the non-playing characters on your latest videogame are AI.  
And yet, these four types of artificial intelligence are very different from each other.

ChatGPT is an LLM, a transformer-based architecture with billions of parameters.  
The image processing algorithms on your phone are likely small and efficient convolutional neural networks designed to work with the computational power of your (relatively) tiny device.  
Recommender systems are quite complicated, and they could use many different kinds of technologies specifically engineered for the field of application.  
The AI of NPCs in video games are often just classical pathfinding and search algorithms, like A*.

Technologically speaking, the knowledge you need to develop any of these AIs is different from each other. Sure, some of the underground fundamentals are the same — in the end, neural networks are almost everywhere — but going back to the figurative examples used in the image above, you can say that both the car and the bike use wheels, but you wouldn’t call a bike shop to fix your car’s wheel — or a car mechanic to fix the engine of a rocket.

So how do we differentiate between these AIs? The answer is: we don’t.  
Currently, everything is marketed as “Artificial Intelligence” without any clarification of what this means. And this affects the job title too; a person having the “AI engineer” title could literally do everything. I have even seen many people claiming they were AI engineers while they were just using ChatGPT APIs to build their software.

If I start looking for a job as an AI engineer, I would receive job offers of any possible kind of AI out there that I don’t even care about.  
On the opposite side, since I mainly work with images, I could say I’m a Computer Vision Engineer, and I would receive tons of job offers that have nothing to do with AI, since Computer Vision is a far wider field than only AI.

So, what exactly is an AI engineer? Well, I came to the conclusion that it is whatever you want it to be.

---

## Why are you worried that you will be replaced?

It’s an understandable question. I just said that AI is an umbrella term that encapsulates many different kinds of subjects. LLMs like ChatGPT are only a part of what is called AI.  
So why should I be worried?

The thing is, these LLMs and foundation models are becoming so general that they are starting to include way more domains under their “side” of the AI world. Just a few days ago, Meta released their new version of DINO, a versatile, powerful and efficient vision model that could be easily applied to different tasks with very little work. Without using annotations and with very good performances. No more need to do research about a certain topic — you already have a plug-and-play solution that will probably work for many applications.

This is the direction AI is taking: cannibalizing all the other branches of AI into general models that can be applied to everything. Why bother tailoring a solution to a specific problem when you can just use the latest generalization breakthrough from big tech? We’ll eventually reach a point where having AI engineers and researchers will no longer be convenient for most companies. The best AI researchers will be concentrated in big tech, and the rest of the market will be highly saturated. Tailored AI solutions will become a luxury that most companies will happily avoid.[^2]

Luckily, this isn’t the case yet. General models still aren’t specialized enough for many domains — especially when data from those domains is scarce or difficult to obtain. It’s not possible to achieve the best outcomes by only relying on a general model. But give it a few years, and this will change. Models will become so general that with only a small sample from the domain you want to apply them to, they’ll quickly specialize for that application.

Most AI engineers will be replaced by AI sooner than software developers, who will still be needed to integrate these AI models into applications.  
And I don’t think AI agents can steal their jobs completely — not yet, at least. Someone still has to use the AI to build the application they want, and that person needs the knowledge to ensure the AI is doing the right thing in the best way possible. This isn’t something AI can fully replace, since agents need a user, and that user has to know what they’re building.

But this is the topic for a different post. :)


[^1]: I do not personally know the authors, and I am not affiliated with them in any way. The purpose of the link is only for credit to the authors — I gain nothing from it.
[^2]: In my opinion, this will also bring a flattening of the curve of AI progress, as there will be fewer and fewer AI engineers, leading to fewer ideas and research, with only a niche of very experienced and stubborn (as most seniors are) engineers working in the field.



