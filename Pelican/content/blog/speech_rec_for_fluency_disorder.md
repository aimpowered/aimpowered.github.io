Title: Speech recognition and enhancement for atypical speech
Date: 2021-03-28
Modified: 2021-03-28
Category: Blog
Tags: Speech-impediment, ASR, wav2vec, kaldi
slug: blog/atypical-speech-autotune
Authors: Shaomei Wu
Summary: I play with a few SOTA speech recognition models with my own speech sample and find a way to auto-tune my own speech to reduce disfluency.

Speech recognition technology has progressed a lot in recent years, especially when using modern deep learning techniques. While new models such as Facebook AI Research's [wav2vec](https://github.com/pytorch/fairseq/tree/master/examples/wav2vec) has achieved 2.43 WER in research benchmark dataset, their performance usually tanks when processing atypical speech, such as, speech by people with fluency disorder, stuttering, people who are deaf or hard of hearing, and people with a thick accent. 

I am one of [many](https://twitter.com/kenjilopezalt/status/1295630888600928258) who suffer from speech [fluency disorder](https://www.asha.org/practice-portal/clinical-topics/fluency-disorders/). How it manifests varies widely for individuals, but as for me, it results in a lot of pauses/breaks and filler words in my natural speech, and it is a lot worse when I am speaking under pressure or are being recorded.

Here is a speech sample of me introducing myself, just to give you a flavor.

<audio controls>
<source src="/media/short_intro.wav">
Audio element failed...
</audio>


You can hear lots of uh's and um's in my speech. While I have been work towards accepting my speech pattern and rolling with it, it does cause some inconvenience in my life. For example:

- Speech-based AI interfaces have trouble understanding me;
- When there is a time limit, I can not fit as much content during my time slot as others do;
- People are often confused and distracted by my atypical speech pattern thus pay less attention to what I say;
- It is very hard for me to leave voicemail... 

## ASR on Atypical Speech

I tried out a few different ASR models to transcribe what I was saying on the audio clip above. 

For easier comparison, here is the manual transcription of my speech:

> Hi my name is Shaomei Wu and I um worked at Facebook. Um my research is at the intersection of um AI and um accessibility. So I try to build empowering AI, um, technology for marginalized communities. 

### wav2vec

I used the pretrained wav2vec2-base-960h model as documented [here](https://github.com/pytorch/fairseq/blob/master/examples/wav2vec/README.md#use-wav2vec-20-with-transformers). And here is the result:

> HI MY NAME IS CHARMARU AND I AM WORK AT FACEBOOK AND MY RESEARCH IS AT THE INTERJECTION OF AM A I AND AM OCCESSIBELITY SO I TRIE TO BEUDE EMPOWERING A I AM TECNOLOGY FOR MAGONOLIZED COMMUNITIES


Since wav2vec is a char-based model, the transcription contains lots of mispellings and non-words. It is definitely hard to understand what I was saying. 

### Google Cloud API

Google Cloud's [speech-to-text API](https://cloud.google.com/speech-to-text/docs/async-time-offsets) gives more readable transcriptions, together with timestamps.

> hi my name is Joe and I worked at Facebook and my research is at the intersection of AI and accessibility so I tried to go to empowering a I realized community
  
One thing I do not really like about this transcription, despite its readability, is how it dropped all the filler words. We will discuss this further in the next session.


### SpeechBrain

[SpeechBrain](https://speechbrain.github.io/about.html) is a open-sourced speech recognition toolkit developped and maintained by a large group of academic researchers. It has a bunch of pretrained models that can be easily loaded from huggingface, and the transcription it provides is this:

> AYE MY NAME IS SHALL I RUIN I I'M WORKED AT FACE BOOK AND MY RESEARCH IS AT THE INTERSECTION OF AH AYE AND I'M ACCESSIBILITY SO I TRIED TO BUILD EMPIRE IN A TECHNOLOGY FOR MAGINALISED COMMUNITIES

It does run a lot slower than wav2vec or Google cloud speech API, but it seems to achived a good balance between readability and authenticity.


### Better ASR for Atypical Speech

Overall none of these models worked very well with my speech and the WER is significantly higher than what was reported with the benchmark.

One way to improve the performance of current models on my speech is to tune the models. Models like wav2vec are mostly unsupervised and allow you to train the model using raw speech recording only and tune the base model using a relatively small labeled dataset and the model theoretically should improve after tuning.

It is still a lot of work to record and transcribe 30mins or hours of my own speech though. One way to make this easier is through data augmentation, a technique I used when training spellchecker for people with dyslexia. More specifically, we could randomly inject filler words into existing training dataset and feed the model with the pertubated data. But for now let's move on and save this for the next blogpost.

## Auto-tuning Atypical Speech

Given that the most obvious thing with my speech is the use of filler words (uhs and ums), I would like to be able to clean them up automatically.

For this reason, Google's transcription does not work for our use case, since it dropped all the filler words! 

The transcription from SpeechBrain and wav2vec are both workable, as they did catch my "um"s and semi-consistently transcribe them as "I'm" or "AM", respectively. 

### Get timestamps for filler words

So now I just need to search the transcription for the filler words and the exact timeframes when they occur. 

Although Google did provide timestamped transcription, their timestamps were not accurate enough for this purpose. Also, they do not even transcribe the filler words, remember?


SpeechBrain and wav2vec do not provide timestamps for their transcription, but fortunately, we can still align the transcription with the audio file using an open-sourced tool called [gentle](https://github.com/lowerquality/gentle/) (which is built on top [Kaldi](https://github.com/kaldi-asr/kaldi)) and infer the timestamps of each word in the transcription.

### Remove filler words from atypical speech

After finding all the start and end times for "AM" in the wav2vec transcription, it is easy to programmatically edit out all these timeframes from the original audio through python. 

Here is the result auto-tuned audio. You can noticed that most of the filler words are gone.

<audio controls>
<source src="/media/de_filler_short_intro.wav">
Audio element failed...
</audio>

## Auto-tuning Video with Atypical Speech

The similar technique can be used to automatically edit a video to cut out the part with filler words, as shown in this example below.

- [Original Video]({static}/media/intro_video_short.mp4)

<video controls height="400">
<source src="/media/intro_video_short.mp4" type="video/mp4">
Video rendering failed...
</video>


- [Auto-tuned Video]({static}/media/autotuned_intro_video_short.mp4)

<video controls height="400">
<source src="/media/autotuned_intro_video_short.mp4" type="video/mp4">
Video rendering failed...
</video>



Some extra steps to make this work are:

1. Extract the audio track from the video

2. Find the timeframes for filler words in original audio/video.

3. Cut the original video.


Note that this type of close-up video is probably not the best demo for this technique, I expect it works better for more static videos like a slide show or instruction videos.

## Resources 

The code for producing the results can be found in this [notebook](https://colab.research.google.com/drive/1jn8oTaEJRMl9PEKi7jj8zfwnxctxox8u?usp=sharing). 

 
 
