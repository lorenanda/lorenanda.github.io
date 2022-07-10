---
layout: post
title: 6 findings from analysing the Oscars speeches of the best directors
tags: [data science, Python]
comments: true
---

**Cinephiles and lovers of glam rejoice this Sunday – it's Oscars Award Ceremony time!** Due to Corona, this year's 93rd edition was postponed from February to April 25th – the latest in the history of the award. I was personally happy about the delay, because it gave me more time to analyse some data and come up with this blog post.

On this ocassion, I was curious to do some text mining on the acceptance speeches. Specifically, I analysed the speeches of the Best Directors between 1941 and 2019. I used a dataset from [Kaggle](https://www.kaggle.com/unanimad/the-oscar-award) and added missing data for 2017, 2018, and 2019 directly from the [Academy Awards Acceptance Speech database](http://aaspeechesdb.oscars.org/).

In total, 74 Best Directors have been awarded and almost all of them gave acceptance speeches, which I analysed with Python and the NLTK library. You can find the Jupyter notebook [here](https://colab.research.google.com/drive/18lgeB3LHdXg2Ly6cjMi49W5VNlmkqZNc?usp=sharing). Let's see what the words reveal about the Best Directors and the Oscars!

### 1. Average speech length
The speech of a Best Director has 104 words on average, but speeches range widely from 8 to 267 words.

Here's how to calculate the number of words in a text:

```python
directing["words"] = directing['Speech_clean'].str.split().str.len()
```

### 2. Longest & shortest speeches
The longest speech runs at 267 words and was given by Mel Gibson at the 68th Academy Awards in 1995 for his film *Braveheart*. This guy had a looot of people to thank to and seems to have used up all his words for saying pretty much nothing.

The shortest speech was summed up in 8 words by Delbert Mann at the 28th Academy Awards in 1955 for his film *Marty*. I really like his efficient "I came. I won. I thanked." structured speech:
> Thank you. Thank you very much. Appreciate it.

Here's how to find the longest and shortest text in a dataframe with pandas:
```python
directing.sort_values(by="words")
```

### 3. Lexical richness
Lexical richness is a measure of how many unique words are used in the text. Lexical richness is calculated as the total number of unique words divided by the total number of words. The higher the score, the richer the vocabulary–and viceversa. Here's to calculate lexical richness for each speech in the dataframe with Python:

```python
def lexical_richness(text):
    return round(len(set(str(text))) / len(str(text)), 3)
directing["lex_rich"] = [lexical_richness(directing["Speech_clean"][i]) for i in range(len(directing))]
```

The speech with the highest lexical richness (0.408) is Delbert Mann's, the director of *Marty*, awarded in 1955. This means that 40.8% of the words he used are distinct.

At the other end, the speech with the lowest lexical richness (0.034) is Mel Gibson's, the director of *Braveheart*, awarded in 1995. This means that 3.4% of the words he used are distinct.  

### 4. Longest words
The longest words used in directors' speeches have 15 words: *administrations*, *cinematographer*, and *czechoslovakian*.

Here's how to select the longest words in a text:
```python
long_words = [w for w in all_speeches_tokenized if len(w) > 14]
sorted(long_words)
```

### 5. Most common words
The top 10 most common words in all acceptance speeches are: *thank* (201 occurences), *much* (56), *like* (50), *people* (48), *want* (42), *would* (30), *movie* (26), *film* (26), *say* (24), and *many* (22).

Interestingly, out of these 10 words, 3 are nouns (referring to *people* and *film*/*movie*), 2 express large quantities (*much* and *many*), and 5 are verbs that express personal feelings (*want*, *like*) or actions (*say*, *thank*). It's also worth noting that the word *thank* has a significantly higher frequency than the following common words, which is however understandable.

Here's how to find the frequency distribution of words in a text with NLTK:
```python
FreqDist(all_speeches_tokenized).most_common(10)
```

### 6. "Thank" to...
Ok, winners thank a lot, but who do they thank to? It turns out... to *you*, but also to *the Pacific Command of the United States*, *Mr. harry Cohn*, *Marlon*, *the producers*, and *each one of them*.

Here's see the location of a word in context with NLTK:

```python
Text(word_tokenize(all_speeches)).concordance('thank')
```

That's all, folks!