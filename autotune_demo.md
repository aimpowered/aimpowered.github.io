---
layout: default
title: "Autotune Demo"
summary: "A demo for autotuning my own speech in audio and video to reduce disfluency."
---

# Use AI to autotune audio and videos with speech disfluencies

*Disclaimer*: This demo is intended as a technical exploration only. We are absolutely not suggesting that speech disfluencies should be hidden or eliminated. We believe everyone should have control over their speech and have a choice on whether and how to share their identity as a person who stutter or with other speech related challenges. We also firmly believe that it is healthy and productive for our society to hear more stuttering collectively and to expand the space for speech disfluencies in our communications.

## Auto-tuning Audio with Speech Disfluencies

Original audio recording of speech with disfluencies (mostly filler words):

<audio controls>
<source src="assets/media/short_intro.wav">
Audio element failed...
</audio>

Original transcription (there are lots of um's): 

> Hi my name is Shaomei Wu and I, um, worked at Facebook. Um, my research is at the intersection of, um, AI and, um, accessibility. So I try to build empowering AI, um, technology for marginalized communities. 

Autotuned version:

<audio controls>
<source src="assets/media/de_filler_short_intro.wav">
Audio element failed...
</audio>

## Auto-tuning Video with Speech Disfluencies

Original video recording of me speaking (12 sec):

<!-- - [Original Video, 12sec](assets/media/intro_video_short.mp4) -->

<video controls height="400">
<source src="assets/media/intro_video_short.mp4" type="video/mp4">
Video rendering failed...
</video>

<br>

Autotuned version (10 sec):

<!-- - [Auto-tuned Video, 10sec](assets/media/autotuned_intro_video_short.mp4) -->

<video controls height="400">
<source src="assets/media/autotuned_intro_video_short.mp4" type="video/mp4">
Video rendering failed...
</video>


## Resources 

Read the [blogpost](2021/03/28/speech_rec_for_fluency_disorder.html) for more details on how the autotuning works.

The code for producing the results can be found in this [notebook](https://colab.research.google.com/drive/1jn8oTaEJRMl9PEKi7jj8zfwnxctxox8u?usp=sharing). 

 
 
