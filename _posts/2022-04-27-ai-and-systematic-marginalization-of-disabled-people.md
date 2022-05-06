---
layout: default
title: "AI and Systematic Marginalization of Disabled People"
Date: 2022-04-27
Modified: 2022-04-27
Category: Blog
Tags: AI, marginalization, representation, disabilities, social justice
Authors: Shaomei Wu
Summary: "I was invited to talk to students from Columbia University about the challenges and marginalizations created by AI technology for disabled people, as part of the Columbia Data for Social Good monthly event."
---

I had the pleasure to speak to students from the Columbia Data for Social Good club in their [monthly event](https://www.linkedin.com/posts/columbiadsg_socialgood-datascience-dataanalytics-activity-6922423431682560000-iwZx?utm_source=linkedin_share&utm_medium=member_desktop_web) on April 27, 2022. Under the theme of Equity for Marginalized Communities using Tech, I discussed the issues, challenges, and opportunities with AI for disabled people. 


Here is an outline of my talk ([slides](https://medium.datadriveninvestor.com/sidewalk-toronto-and-why-smarter-is-not-better-b233058d01c8))

### 1. The promises of AI for disabled people.
There has been quite a lot of discussions and awareness regarding AI biases and harms towards women and racial minorities. However, when it comes to disability, AI is often portraited as a magic pill that will *help* or *solve* disabilities once for all, often by compensating human abilities and acting as the "eyes" or "ears" for people with disabilities. This vision of AI, although possible, is superficial if not misleading given what we have seen in the development and delopyment of AI technologies so far.

### 2. The problems 
I argued that there are two sets of problems AI has imposed on disabled people.

First, many AI advancement does not function with or benefit people with disabilities. Take the speech recognition model as an example, despite its recent advancement, it still works poorly for me as a person who stutter, and causing lots of frustrations and sommetimes fear when the voice interfaces are delopyed more and more widely.

Second, not only do AI systems not benefiting people with disabilities, they can also actively punish and harm people with disabilities. For examples, researchers found that sentences containing disability-related words are more likely to be predicted as "toxic" by Google's perspective API, which are used widely by lots of other platforms. TikTok also openly admitted that they downrank the videos containing disabled people, in the name of protection and anti-bullying. Algorithmic decisions like this suppress the existence of disabled people and deny our access to public spaces.  

### 3. Factors contributing to AI-powered marginalization of disabled people.
Yes, the discriminations towards disabled people exist in the world before AI came to play, but I think AI systems not only reflect the existing biases but also exerbate them. And excerbation is realized in many different places in AI pipleine, including data, methodology, and evaluation metrics.

  - Data: people with disabilities are under-represented and often misrepresented in the data used to train AI models. As a result, the model's performance degraded when used by people with disabilities, or the model produces unfavorable predictions for people with disabilities.

  - Methodology: modern ML relies on regularities and pattern in the data, as a result, most models pick up the "center" areas of the distribution and ignore the "outliers" in the periphery.

  - Metrics: most of the standardized benchmarking metrics do not align with the subjective experience of people who are most impacted by these metrics. Take Image captioning as an example, lots of investments have gone into this domain, using assisting people with visual impairements as an aspiration. However, the common metrics used to benchmarking image captioning models, such as BLEU and CIDER, are only measure syntaxt similarity between prediction and the label, without considering the impact of generated captions to people who can't see the images. When people can not see the image to verify how accurate the caption is, and were instructed to trust the "AI", some captions can have very negative impact when consumed by people with visual impairements, causing feelins like confusion, self-doubt, embarressment...

### 4. What can we do
I want share a few techniques to address the issues we discussed above, all driven by the guilding principle of "nothing about us, without us". We need meaningful representation of the lived experience of marginalized groups in every step of the AI develepment pipeline.

  - *Representation in Data*. Some tech companies have been soliciting data from people with disabilities to enhance their AI models. Google's project Euphonia is a good example through which they ask people with atypical speech to record and donate their speech samples. The effectiveness of such approach might be limited due to the lack of trust and privacy concerns of the disabled communities, which is understandable given the history of tech companies harvesting and misusing personal data from minority and marginalized groups. I hope there can be more grassroot movements led and driven by the disability communities, through which we can collect, manage, and use the data about us for our needs.

  - *Representation in sampling method*. To surface outliers and avoid the majority overwhelmed the marginalized users, Jutta Treviranus proposed the method of "Lawnmower of Justice", which I found elegant and intriguing. The basic idea is to downsample the dense parts of the dataset to force the model to pay attention to the outliers.

  - *Representation in metrics*. There has been some research efforts to develop human-centred evaluation metrics for AI models. For example, the work by MacLoed, Bennett, Morris, and Cutrell proposed a new metric - congruence - for image captioning model that measures how sensible a generated caption is in the context of the image. If used as a benchmarking metrics, it can force the model to pay some attention to the potential confusion that can be caused by the generated captions.    

### 5. Beyond equality
Fixing all existing biases and discriminations embedded in current systems may lead us to equality. However, to achieve equity, we need to actively push the envelope and envision new things that deliver tangible benefits and level the playing fields. I share a few of my previous projects as example of how I think about equitable technology for disabled people.

 - [Automatic alt-text](https://research.fb.com/wp-content/uploads/2017/02/aat_cscw2017_camera_ready_20161031-2.pdf). This is a feature I developed on Facebook that uses computer vision to describe images for screen reader users of Facebook and Instagram. We made the deliberate decision to not use the off-the-shelf image captioning models because of the issues with those models we discussed above. Instead, we oriented the design and development of the model towards the needs of blind users to "glance through" their feeds and get basic information about the images before interacting with them (same as most people!). And we collaborated closely with visually impaired users on all the design decisions, such as what to describe, in what order, what are the acceptable precision, etc. 

  - [Writing assistance](https://research.fb.com/wp-content/uploads/2019/02/Design-and-Evaluation-of-a-Social-Media-Writing-Support-Tool-for-People-with-Dyslexia.pdf). This is an experimental grammer/spellchecking tool developed in collaboration with the dyslexia community. Different from most on the market spellcheckers, we trained and benchmarked the model using data specific to dyslexia style writing to prioritize the needs of users with dyslexia, who are mostly impacted by spellcheckers and often face additional challenges when writing on social platforms.  


I had a great discussion with students in the Data for Social Good event afterwards. We talked about the collaboration between tech and disability rights activism, the incentives for tech companies to push for progress, and the ways orient our analytics skills towards ethical values and societal benefits.
 
