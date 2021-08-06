---
layout: post
title: Fear and loathing in Romanian (psych-verbs)
subtitle: Research study
gh-repo: lorenanda/psych-verbs
gh-badge: [star, fork, follow]
tags: [data science, linguistics, projects]
comments: true
---

I've been interested in emotions ever since I've become aware of them. Maybe because I was unsure how to process and interpret them, in both myself and others. How do people express emotions and why do they do it so differently? Is *being scared* the same as *fearing*? Can I really understand or experience *sirva vigad* if the word doesn't exist in my native language?

My solution to deal with this personal struggle was to read and research about emotions. I know I know, you can't learn everything from books, especially not human feelings and interactions, but nevertheless I've discovered some fascinated learnings about emotions.

This is why in university I chose to research verbs of emotion, more specifically to investigate the semantic characteristics of Romanian verbs of emotion.

The project was conducted during my Master's degree in Linguistics at Humboldt-Universität zu Berlin and was also inspired by the research of [Prof. Elisabeth Verhoeven](https://www2.hu-berlin.de/experiencer/alternation/en/index.html) and [Hartshorne et al.](https://www.researchgate.net/publication/308761372_Psych_verbs_the_linking_problem_and_the_acquisition_of_language) on psych-verbs in different languages.

Since 2018, when I started working on this project, I've had the chance to present some preliminary findings at the [5th Linguistik Meetup in Potsdam]({% post_url 2018-08-04-poster-linguistik-meetup-potsdam %}) and apply newly-learned [machine learning models](https://github.com/lorenanda/psych-verbs) for analyzing the data. 

In this blog post, I want to share with you the fascinating topic of psych-verbs, how I designed my research experiment, how I analyzed the collected data, and most importantly what I found out about Romanian psych-verbs. 

## A brief theory of psych-verbs 

**Psych-verbs** (also psychological verbs or experiencer verbs/predicates) express the mental state or emotion of an experiencer. The experiencer role refers to a participant that undergoes an event affecting consciousness. The experiencer can appear in one of two positions: as subject (**subject experiencer - SE**) or as object (**object experiencer - OE**). Take for example two illustrative sentences:

|*Jack scares Wendy.*|*Wendy fears Jack.*|
|--------------------|-------------------|
|Wendy is the OE of an action (emotion) inflicted by Jack upon her.|Wendy is the SE of an emotion that arises within her in response to Jack being perceived as a threat.|

<figure><img src="https://screenqueens.files.wordpress.com/2014/06/1.jpg" alt="Here's Johnny!" style="width:100%"><figcaption align = "center"><i>Here's Johnny!</i></figcaption></figure>

Even though the two verbs express the same emotion of fear, they have different syntactic structures, depending on the experiencer form. 

This structure appears to be unsystematic across languages, so there are no clear rules for which verbs are either OE, SE, or both. For this reason, psych-verbs pose a linguistic challenge in explaining the link between syntax and semantics. 

At the point of writing (early 2019), theoretical and experimental research has limited to popular languages (e.g., English, German, Japanese) and there are no experimental studies on Romanian psych-verbs. This is unfortunate, because native speakers' intuition can provide insights into a language. 

Therefore, my aim was to fill this research gap by conducting an experiment that reveals the semantic properties of psych-verbs in my native language, Romanian.

## How I researched Romanian psych-verbs
To research how people perceive psych-verbs, I designed an experiment, carried it on native Romanian speakers, and analyzed the resulted data.

### Designing the research experiment
I composed a list of 54 Romanian verbs myself. I chose verbs that have been included in research studies in other languages, but also new verbs that haven't been investigated before. Importantly, I assigned the verbs to six emotion categories (based on [Paul Ekman's theory of basic emotions](https://www.tandfonline.com/doi/abs/10.1080/02699939208411068)): anger, disgust, fear, happiness, sadness, and surprise.

Each verb had to be rated from 1 (least) to 5 (most) on four criteria: 
- **valence**: whether the verb expresses a negative or a positive emotion
- **arousal**: how intense is the emotion expressed by the verb)
- **duration**: how long is the emotion expressed by the verb likely to last
- **cause**: whether the emotion expressed by the verb is perceived to be caused by external or internal factors

### Getting participants
For this experiment, I selected participants through word of mouth. I gave them the verb list in paper-form or sent email it to them, and asked them to complete it in one sitting. The verb list was randomized for each participant, so that the order of the verbs could not influence the ratings. 

In total, I had 30 participants:
- all native speakers of Romanian
- 17 females, 6 males (self-identified)
- 32 years old on average

## Analyzing the data
After collecting responses from each participant, I went into the deep work: analyzing the data. I did all data analysis in Python with libraries such as pandas, seaborn, and scikit-learn. If you're interested in seeing the detailed data analysis, check out this [Jupyther Notebook](https://github.com/lorenanda/psych-verbs/blob/master/psych-verbs.ipynb).

### Descriptive analysis
First, I ran a **descriptive analysis**, where I looked at the distribution of values by experiencer, emotion domain, feature rating, and verb. At this stage, I was interested in answering questions like:
- How long do happiness emotions last on average?
- What is the most intense emotion domain?
- Are SE verbs more positive than OE verbs?
- Is there a correlation betwee the duration and valence of an emotion verb?

<figure><img src="../assets/img/psychverbs_cumplot.svg" alt="psych verbs descriptive analysis plot" style="width:100%"><figcaption align = "center"><i>Pair plot of psych verbs by feature</i></figcaption></figure>

The pair plot above depicts three histograms of Duration, Arousal, and Value, as well as six scatterplots with regression lines of the combinations of the three features.

### Clustering
Second, I used **K-Means clustering** to identify clusters of verbs based on their duration, arousal, and valence ratings. The question here was whether some emotion verbs are closer (i.e. more similar) based on their values, rather than on the emotion category they belong to. The K-means

<figure><img src="../assets/img/psychverbs_kmeans.svg" alt="psych verbs kmeans" style="width:100%"><figcaption align = "center"><i>K-Means clustering of psych-verbs by feature</i></figcaption></figure>

The scatterplot represents the three verb clusters formed based on the three features Duration, Arousal, and Valence.

- The blue-marked cluster represents verbs with low values, concentrated in the lower left corner of the graph.
- The red-marked cluster represents verbs with average values, concentrated at the middle of the y-axis and along the x-axis.
- The green-marked cluster represents verbs with positive ratings, concentrated in the center and upper right corner of the graph.

K-Means clustering has some limitations: it builds clusters of the same size and we need to specify the number of clusters in advance.

As an alternative to K-Means clustering, I also generated a dendogram to illustrate **hierarchical clustering**, or what is the distance between verbs based on their duration, arousal, and valence values.


<figure><img src="../assets/img/psychverbs_dendrogram.svg" alt="psych verbs dendrogram" style="width:100%"><figcaption align = "center"><i>Hierarchical clustering (dendrogram) of psych-verbs</i></figcaption></figure>

The x-axis represents the indices of the verbs and the y-axis represents the distance between the verbs. The vertical blue line build the maximum distance. I choose a threshold of 8 to separate the maximum distance and thus form two main clusters (orange and green), or three considering the two green subclusters separate.

The dendrogram shows how close verbs are to each other, based on the three features.

In the first orange cluster, there are 5 pairs of directly related verbs:

    to panic (24) - to surprise (50)
    to get angry (32) - to amaze (51)
    to fascinate (8) - to fear (44)
    to impress (10) - to get annoyed (43)
    to satisfy (30) - to suffer (48)

In the second green cluster, there are 7 pairs of directly related verbs:

    to like (25) - to reject (29)
    to wish (6) - to love (20)
    to frustrate (9) - to provoke (28)
    to sadden (17) - to stress (47)
    to annoy (7) - to frighten (13)
    to bring joy (1) - to please (11)
    to depress (2) - to rejoice (31)

In the third green cluster, there are 8 pairs of directly related verbs:

    to disgust (4) - to irritate (19)
    to amuse (0) - to be ashamed (41)
    to get scared (42) - to shock (45)
    to shadder (12) - to humiliate (52)
    to brighten up (18) - to shadder (33)
    to wonder (22) - to offend (23)
    to get sad (36) - to brighten up (37)
    to bore (26) - to get bored (40)


### Classification / Regression
Third, I attempted to classify psych-vers by using K-Nearest Neighbor (KNN), logistic regression (LR), decision trees (DT), and random forest classifiers. I say "attempted" because I was aware from the start that my data set was way too small to be fit for ML models, so I was expecting low results.

|model|accuracy|
|-----|--------|
|KNN|41.18%|
|LR|70.37%|
|DT|72.73%|


<figure><img src="../assets/img/psychverbs_decisiontree.svg" alt="psych verbs decision tree" style="width:100%"><figcaption align = "center"><i>Decision tree for psych-verbs</i></figcaption></figure>

## Findings on Romanian psych-verbs
### Means
- The average and median **duration** of the verbs is 2.2, and most commonly 1.8, so the verbs in the dataset express emotions that are perceived to last only a short time.
- The average, median, and mode of **arousal** is around 3.3, which means that the verbs express emotions that are not particularly intense.
- The average **valence** of the verbs is 2.6, but most ratings are 1.9 and the most common rating is 1.55. This means that the selected verbs express mainly negative emotions.

### Correlations
- There is a **positive correlation** between Arousal and Duration, i.e. verbs with high levels of arousal tend to last longer.
- There is a **negative correlation** between Valence and Duration, i.e. verbs with negative meaning tend to last a short time.
- There is **no correlation** between Arousal and Valence.

### Experiencer
- While OE and SE verbs have similar Duration and Arousal values, they differ significantly in terms of Valence. OE verbs have low Valence (mean 2.18, median 1.75), whereas SE verbs have positive Valence (mean 3.19, median 3.55). This means that emotions that are caused by external factors are perceived as negative, whereas emotions that arise within the experiencer are rather positive.

<figure><img src="../assets/img/psychverbs_experiencer.svg" alt="psych verbs by experiencer" style="width:100%"><figcaption align = "center"><i>Pair plot of psych-verbs by experiencer</i></figcaption></figure>

### Emotion domains
- The emotions that last longest express Happiness in SE form, and the shortes ones express Fear in SE form.
- The verbs with extreme Arousal levels express Happiness but also Sadness, in both OE and SE form. The most intense emotions, both positive and negative, belong to the Happiness and Sadness domains.

<figure><img src="../assets/img/psychverbs_domain.svg" alt="psych verbs by domain" style="width:100%"><figcaption align = "center"><i>Box plot of psych-verbs by domain and feature</i></figcaption></figure>

- The most positive emotions express Surprise in OE form, while the most negative ones express Fear and Anger also in OE form.
- Panic is to Surprise as Satisfaction is to Suffering. 
- Boring someone and being bored feel the same.

## What's next?

### Limitations
Though this experiment revealed new findings, this subject can be explored further. The main limitation of this study is the small sample size of participants. Moreover, it would be interesting to explore how verb ratings differ by gender or age of the speakers.

### Applications of psych-verbs
Initially, my main interest was to explore the linguistic structure of psych-verbs, but while working on the data analysis and reading research on emotions, I realized the findings of my study could be used for natural language processing (NLP) tasks, such as sentiment analysis and emotion recognition. For example, detecting signs of depression or anxiety in texts (e.g., forums, clinical notes).

---
