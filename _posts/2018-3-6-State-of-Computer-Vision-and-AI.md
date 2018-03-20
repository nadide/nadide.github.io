---
layout: post
title: The state of Computer Vision and AI
date: 2015-05-01 12:00
excerpt: Are we really, really far away?
tags: [Algorithms]
comments : true
---

I reviewed a blog post of Andrej Karpathy about state of computer vision and AI. He demonstrated the complexity and scale of the AI and computer vision problems further.  


![](http://karpathy.github.io/assets/obamafunny.jpg)
The picture above is funny.

What would it take for a computer to understand this image as we do?

He challenged expand on all the pieces of knowledge that how picture began to make sense. Here is his short attempt:

- You recognize it is an image of a bunch of people and you understand they are in a hallway
- You recognize that there are 3 mirrors in the scene so some of those people are “fake” replicas from different viewpoints.
- You recognize Obama from the few pixels that make up his face. It helps that he is in his suit and that he is surrounded by other people with suits.
- You recognize that there’s a person standing on a scale, even though the scale occupies only very few white pixels that blend with the background. But, you’ve used the person’s pose and knowledge of how people interact with objects to figure it out.
- You recognize that Obama has his foot positioned just slightly on top of the scale. Notice the language I’m using: It is in terms of the 3D structure of the scene, not the position of the leg in the 2D coordinate system of the image.
- You know how physics works: Obama is leaning in on the scale, which applies a force on it. Scale measures force that is applied on it, that’s how it works => it will over-estimate the weight of the person standing on it.
- The person measuring his weight is not aware of Obama doing this. You derive this because you know his pose, you understand that the field of view of a person is finite, and you understand that he is not very likely to sense the slight push of Obama’s foot.
- You understand that people are self-conscious about their weight. You also understand that he is reading off the scale measurement, and that shortly the over-estimated weight will confuse him because it will probably be much higher than what he expects. In other words, you reason about implications of the events that are about to unfold seconds after this photo was taken, and especially about the thoughts and how they will develop inside people’s heads. You also reason about what pieces of information are available to people.
- There are people in the back who find the person’s imminent confusion funny. In other words you are reasoning about state of mind of people, and their view of the state of mind of another person. That’s getting frighteningly meta.
- Finally, the fact that the perpetrator here is the president makes it maybe even a little more funnier. You understand what actions are more or less likely to be undertaken by different people based on their status and identity.

In a second, we are using huge amount of data from our knowledge. Data about the 3D structure, people identification and object identification, physics (how a specific instrument works), psychology (hoe people think) etc. All these different information  miraculously become meaningful in our brain.

What is amazing that all of the above assumptions come from a brief glance at a 2D array of R,G,B values. There is the point that you can see the iceberg behind the problem. How you can make some sense out of bunch of pixel? How you can use your prior knowledge, even how you can gather information from pixels?

Any using art techniques in computer vision isn't perfectly working, even it is all specific, disconnected, and only half works. Andrew states "The road ahead is long, uncertain and unclear."

And he concluded that computer to understand this image as we do that allow them to get exposed to all the years of experience we have, ability to interact with the world, and some magical active learning/inference architecture.

Are you agree with him? Are we really far away?
