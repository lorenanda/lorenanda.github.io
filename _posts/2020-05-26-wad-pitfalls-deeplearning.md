---
layout: post
title: The Pitfalls of Deep Learning
subtitle: We Are Developers
tags: [data science, events]
comments: true
---

We Are Developers is the world’s largest conference for software development. It’s a great opportunity for software engineers to connect with tech companies and learn about interesting advances in technology. This year, WAD was supposed to take place in Berlin, but due to COVID-19, the event was moved online for a Live Week (25-29 May) of exciting talks on different tech topics.

On the second day, I tuned in to watch **Adrian Spataru‘s and Bohdan Andrusyak‘s talk *The pitfalls of Deep Learning – when Neural Networks are not the solution***.

Adrian and Bogdan are data scientists specialized in time series and computer vision, and NLP respectively. They also organize the Machine Learning Meetup in Graz, Austria.

For a start, they presented a comparison between Machine Learning (ML) and Deep Learning (DL):

- ML goes from data to feature extraction to a ML model and finally to an output. Examples of ML are SVM, gradient boosting, and linear regression.
- DL goes from data to DL (with very powerful feature extractors) and to the output. Examples of DL are convolutional neural networks, recurrent neural networks,  and transformers.

Next, they gave three examples of DL applications:

- **self-driving cars**: arguably wouldn’t be possible without DL, which are very good feature extractors.
- **language translation**: DL is very very good at representation learning and has high computational power to find representations faster.
- **music generation**: DL allows to model complex sequence data, which makes it possible to generate high dimensional data.

Amazing as DL may sound, it has also produced failures, such as:

- **criminal identification**: In 2019, Amazon’s facial recognition system Rekognition was tested on the faces of 24 professional football players and it shockingly matched almost 1 in 6 players with a mugshot in the police database.
- **mistranslation**: A Zalando ad for lingerie which had in its original text the cuddle word “baby” was wrongly translated (and targeted) as “kid”.
- **false claims**: Many companies claim (or naively conclude) to have used DL to solve problems that actually are not possible (yet), like predicting IQ, sexuality, or even whether a person is a potential terrorist.


The key idea of the presentation were the five issues with DL:

- **data quantity and quality**: DL models can be only as good as the data they use – if with insufficient and unclean data they could only produce skewed results.
- **tabular data (spreadsheets)**: is limited and as an alternative, tree-based models outperform DL, especially with good feature engineering.
- **model explainability**: automatic feature extraction gives less control over the model.
- **model complexity**: sometimes complex models can’t be used in real-life systems.
- **resources**: the more parameters the model has, the more expensive it becomes.


In conclusion, those excited about integrating DL solutions in businesses are advised to not jump into it, but first think in terms of business gain: whether the performance boost that DL would provide is worth for the business. It’s more advisable to start with benchmarking and ML and see where they can go from there.
