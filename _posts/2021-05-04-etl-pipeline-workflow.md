---
layout: post
title: Automate your data processing pipeline in 9 steps
tags: [tutorial, n8n]
share-description: Learn how to build an n8n workflow that processes text, stores data in two databases, and sends messages to Slack.
canonical_url: https://n8n.io/blog/automate-your-data-processing-pipeline-in-9-steps-with-n8n/
---

If you've ever struggled with setting up pipelines for extracting, transforming, and loading data (so-called ETL jobs), managing different databases, and scheduling workflows -- know that there's an easier way to automate these data engineering tasks.

In this tutorial, you'll learn how to build a no-code n8n workflow that processes text, stores data in two databases, and sends messages to Slack.

## The data pipeline

A few months ago, I completed a Data Science bootcamp, where one week was all about data engineering, ETL pipelines, and workflow automation. The project for that week was to create a database of tweets that use the hashtag #OnThisDay, along with their sentiment score, and post tweets in a Slack channel to inform members about historical events that happened on that day. This pipeline had to be done with [Docker Compose](https://docs.docker.com/compose/) and included six steps:

1.  Collect tweets with the hashtag #OnThisDay
2.  Store the collected tweets in a [MongoDB](https://www.mongodb.com/) database
3.  Extract tweets from the database
4.  Process the tweets (clean the text, analyse sentiment)
5.  Load the cleaned tweets and their sentiment score in a [Postgres](https://www.postgresql.org/) database
6.  Extract and post tweets with positive sentiment in a [Slack](https://slack.com/intl/en-de/) channel

![](https://n8n.io/blog/content/images/2021/04/ETL_pipeline_simple2-1.png)


## The workflow with Python

This is a fun project that offers lots of learning opportunities about different topics: APIs, text processing with Natural Language Processing libraries, both relational and non-relational databases, social media and communication apps, as well as workflow orchestration.

If you're wondering, like I did, why we had to use two different databases, the answer is simple: for the sake of learning more. Postgres and MongoDB represent not only different database providers, but different kinds of database structures -- [relational (SQL) vs non-relational (NoSQL)](https://www.mongodb.com/nosql-explained/nosql-vs-sql) -- and it's useful to be familiar with both.

Though our use case is just for fun, this pipeline can support most common data engineering tasks (e.g. aggregating data from multiple sources, setting up and managing the data flow across databases, developing and maintaining data pipelines).

I was really excited, though also a bit overwhelmed by all the things I had to set up for this project. In total, I spent five days learning the tools, debugging, and building this pipeline with Python (including libraries like [Tweepy](https://www.tweepy.org/), [TextBlob](https://textblob.readthedocs.io/en/dev/), [VADER](https://github.com/cjhutto/vaderSentiment), and [SQLAlchemy](https://www.sqlalchemy.org/)), Postgres, MongoDB, [Docker](https://www.docker.com/), and [Airflow](https://airflow.apache.org/) (most frustrating part...). If you're interested to see how I did this, you can check out the project on [GitHub](https://github.com/lorenanda/tweets-docker-pipeline) and read [this blog post](https://lorenaciutacu.com/2020-11-14-bootcamp7/).

But in this article, I'll show you an easier way to achieve the same result in as much as an hour -- with a **no-code workflow** in n8n!

## The workflow with no code

Since I started using n8n, I've been looking for use cases for various data science tasks, starting with my existing projects. When I realised that all the apps and services that I used in my tweets pipeline are available as n8n nodes, I decided to replicate the project as an n8n workflow with nine nodes:

1.  [Cron node](https://docs.n8n.io/nodes/n8n-nodes-base.cron/) to schedule the workflow
2.  [Twitter node](https://docs.n8n.io/nodes/n8n-nodes-base.twitter/) to collect the tweets
3.  [MongoDB](https://docs.n8n.io/nodes/n8n-nodes-base.mongoDb/) to store the tweets
4.  [Google Cloud Natural Language](https://docs.n8n.io/nodes/n8n-nodes-base.googleCloudNaturalLanguage/) to analyse the sentiment of the tweets
5.  [Set](https://docs.n8n.io/nodes/n8n-nodes-base.set/) to extract the sentiment values
6.  [Postgres](https://docs.n8n.io/nodes/n8n-nodes-base.postgres/) to store the tweets and their sentiment
7.  [IF](https://docs.n8n.io/nodes/n8n-nodes-base.if/) to filter positive and negative tweets
8.  [Slack](https://docs.n8n.io/nodes/n8n-nodes-base.slack/) to post tweets into a channel
9.  [NoOp](https://docs.n8n.io/nodes/n8n-nodes-base.noOp/) to ignore negative tweets

![](https://lh6.googleusercontent.com/F42x14NNPvLbk_b68rOkkpXQDLRegGXTOjkK3PONzLJxPdoaAquCW32eYMzM0aLO2svLcCvv7txB8km2DWg7H7i55AmR67u2b624CXf_hXqfogfpEbCjS6poAxIu235bQ6UtJUVC)

In this article, I'll show you how to set up this workflow node by node. If this is your first n8n workflow, have a look at our [quickstart guide](https://docs.n8n.io/getting-started/quickstart.html) to learn how to set up n8n and how to navigate the Editor UI. It's also helpful to have at least basic knowledge of databases and SQL.

Once you have your n8n Editor UI open, there are two ways to follow this tutorial: either copy the workflow from [here](https://n8n.io/workflows/1045) into your Editor UI and deactivate the nodes, so that you can execute and test each node separately, or add the nodes one at a time.

### 1\. Starting the workflow

We will begin with the end in mind: We know that we want this whole workflow to run every day, so first we need to set up the **Cron node** to trigger our workflow every day at 06:00.

![](https://lh4.googleusercontent.com/fY39vU3j9UgE-kZa7oCbuGLckzIYtlhGxNIYXpraCR7SljiX1t9zpwOp0rd6-agoXRY6RS4c3N4P7gpwG9lQE5D55WMvRaaYrEYfHOqjWf0oUMIuxW1gPOC8RxolI3JbB46NUqJg)


The Cron node makes it very easy to schedule and trigger workflows, compared to setting up [scheduling and triggers in Airflow](https://airflow.apache.org/docs/apache-airflow/1.10.1/scheduler.html), and this saved me so much time and nerves!

### 2\. Collecting tweets

Next, we are going to collect tweets with the hashtag #OnThisDay. To do this, first you need to create a [Twitter Developer](https://developer.twitter.com/) account and register an app. Follow the instructions [in our reference docs](https://docs.n8n.io/credentials/twitter/) to learn how to set up your Twitter app and get the necessary credentials (Consumer Key and Consumer Secret). Once you have your credentials, copy and paste them in the ***Credentials*** field of the **Twitter node**. Next, set the parameters:

-   *Operation*: Search
-   *Search Text*: #OnThisDay
-   *Limit*: 3. This last step is not mandatory, but I recommend limiting the number of collected tweets at least for testing the workflow, to ensure that you don't reach the query rate limit of the Twitter API and Google Cloud Natural Language.

![](https://lh4.googleusercontent.com/PeJmypmy2yeLPl6LUmqTdVOlYI3tU-gc4LNfO8WSWKxor8wotBiaNYVbYoJbVMKHDfXlDRH1EHQW2OXnsqYoIQE-YrVjlAcyMIxfUToopAaERnM9UJKHszGPMpCC_jedmI04lu8K)

### 3\. Inserting tweets into MongoDB

Now that we collected some tweets, we need to store them into a database. MongoDB is a non-relational database (NoSQL) that stores data in JSON-like documents. Since our tweets are returned in JSON format, MongoDB is the ideal database to store them in and the **MongoDB node** allows us to connect to the database. Before configuring the node, you need to create a MongoDB instance, set up a cluster, create a database and a collection within it.

1.  [Create a MongoDB account](https://account.mongodb.com/account/register)
2.  Set up a cluster: *cloud.mongodb.com  Clusters  Create New Cluster*
3.  Create a database: *Cluster  Collections  Create Database*
4.  Create a collection: *Cluster  Collections  Database  Create Collection*
5.  Create a field: *Collection  Insert document  Type the field "text" below "_id"*
6.  Allow access to the database: *Project  Security  Network Access  IP Access List  Add your IP address.*
7.  Connect to the database from your terminal:\
    *mongo "mongodb+srv://YourClusterName.mongodb.net/YourDatabaseName" --username YourUsername*

If you need more detailed information or other set up options, refer to the [MongoDB documentation](https://docs.atlas.mongodb.com/connect-to-cluster/). Now that we have a MongoDB collection up and running, we can set up the MongoDB nodefor our workflow. Set up:

-   *Connection String*: mongodb+srv://YourClusterName.mongodb.net/YourDatabaseName
-   *Database*: YourDatabaseName

![](https://lh4.googleusercontent.com/bZKvOmb77F_53sYOrMb9vhozRKP9ONC7_GXTx3yRwGpA3QZIx-mK7JY-El3W_n7kzrNo4GTB6_yOfUgTyJ39ki3wrrbEv1b4z_UeWIq7qB_sVLhUWo1sIWOQmkhbkMn-Kz0vw0VI)


Next, configure the node parameters to insert the collected tweets into the collection:

-   *Operation*: Insert
-   *Collection*: YourCollectionName
-   *Fields*: text

![](https://lh3.googleusercontent.com/F4KpCoY7W8hor4N7si5b_U8QBtNiR-cKfBYdMeZIl7AJ00YlsVhWSZmI61yIfU5qFuPi2x0D7jxQeYIJqi1u-75m67AhIFeMSdeNOPkh7aX21ia6Oomz3csSUP-VFoPrX7E1DJiS)

### 4\. Analysing the sentiment of tweets

Here comes my personal favourite part of this workflow: analysing the sentiment of tweets, i.e. the feeling associated with the entire text or entities in the text. For this, we use the **Google Cloud Natural Language node**, which analyses a text and returns two numerical values:

-   **score**: Sentiment score between -1.0 (negative sentiment) and 1.0 (positive sentiment).
-   **magnitude**: A non-negative number in the [0, +inf) range, which represents the absolute magnitude of sentiment regardless of score (positive or negative).

Both results are returned as documentSentiment in JSON format:

```
{
"magnitude": number,
"score": number
}
```

Before configuring the node, you have to sign up on the [Google Cloud Platform](https://cloud.google.com/) to enable the API and get the necessary credentials (Client ID and Client Secret). Follow the instructions in [our reference docs](https://docs.n8n.io/credentials/google/#prerequisites) to set up your account and the node credentials.

Once that's done, add an expression to the parameter *Content* by clicking on the gear icon and selecting *Current Node  Input Data  text*.

![](https://lh6.googleusercontent.com/utW8tHN_ZgvOkw91HB2S63vwMvi4ujHuR2RAQGYw_Q0D2vaTKDFbROda34tQZ2P5zc_pJyt32ZeNE8cML4h4X-CoaGHlkzgI-fG1nWEVN1zknH7KK01ElxP8aPrE02prcX7SUrhj)

As a side note, here it was interesting to see how differently Google Cloud Natural Language and the VADER and TextBlob libraries evaluated the sentiment of text:

|Tweet|GCNL|VADER|TextBlob|
|---|---|---|---|
|#OnThisDay in 2018!Champions League,quarter-final,1st legLiverpool-Manchester City 3-01-0 Salah(12),2-0 Oxlade-Chamber...|0.3|0|0|
|Champions 🏆🏆#OnThisDay in 2016 🎉|0.1|0.7269|0|
|#OnThisDay - 4th Apr 2018 former player, assistant manager &amp; caretaker manager passed away aged 61.3 years #GBNFRa...|0|0|-0.05|

### 5\. Processing sentiment analysis

Now that we have sentiment scores for each tweet, we want to insert the text, sentiment score, and magnitude of the tweets into a new Postgres database. Since the magnitude sentiment score and the magnitude are included in the documentSentiment, we need to extract them in order to insert the values in two separate columns in Postgres.

For this, we use the **Set node**, which allows us to set new values based on the data we already have. In the node parameters, set three values:

-   **Score** (number): *Current Node  Input Data  JSON  documentSentiment  score*
-   **Magnitude** (number): *Current Node  Input Data  JSON  documentSentiment  score*
-   **Text** (string):* **Current Node  Input Data  JSON  sentences  [Item: 0]  text  content***

![](https://lh5.googleusercontent.com/TGiCiuzI7T0I1vzsCKqI9K6HKL040hSPqXMnq-bYgSB3Hp-t6iKXbxc_W8jbg2njiV5BMl8ztpgZbpEAvg1ulpVror7ln-mxIgbYejaDZC8BJW5EafnZILkkxijuHoSr7aO-e4ax)

### 6\. Inserting tweets values into Postgres

Next, we want to insert the newly set data values into a Postgres database. First, you need to [install Postgres](https://www.postgresql.org/download/), then create a database and a table for tweets. The process is quite similar to the MongoDB setup and you can do this from your terminal:

1.  Connect to Postgres:

```
psql

```

1.  Create a database:

```
createdb twitter

```

1.  Go into the created database:

```
psql twitter

```

1.  Create columns in the database. The columns have to be named like the values defined in the Set node, in order to be matched.

```
CREATE TABLE tweets (text varchar(280), score numeric(4,3), magnitude numeric(4,3));

```

Now we can go ahead and configure the **Postgres node**. Fill in the name of your database, username, and password in the *Credential Data* fields, then configure the node parameters:

-   *Operation*: Insert
-   *Table*: tweets
-   *Columns*: text, score, magnitude
-   *Return Fields*: *

![](https://lh4.googleusercontent.com/5A9pkc4DcQO5YE5IOJSPopYst9ELHwcISIDHxnfQI3T2CwZpio5ATw31y-AFCqLVT77EDSALP0Q43cbeBQ9D7G6pXGNTObA9KDexwmoIMNGDv038x0mHqdWEI2jxywKGVJgQscRV)

After executing the node, you can check if the tweets have been inserted in the table by running *SELECT * FROM tweets;* in the terminal.

### 7\. Filtering positive and negative tweets

Here comes another fun part related to sentiment analysis: filtering negative tweets. For this, we use the **IF node**, which allows us to split the workflow conditionally based on comparison operations. We define positive tweets as those with a sentiment score above 0. To configure the IF node with this condition, configure the parameters:

-   *Value 1*: Current Node  Input Data  JSON  score
-   *Operation:* Larger
-   *Value 2:* 0

![](https://lh4.googleusercontent.com/BvZZPOZzhvwmfD9T7Ogs0bnHb5b8dasX2xnAuSD_cppyZ2fWiMFVPV3uo4oUKsAfBabCCvHg4vlbm-RfDrceHdDTse2D0uJ2ncuEOFSwnndptKsa2yqmLb9Av28TKD1O01SAm_XV)

This condition determines the data flow to the following connection: if the sentiment score is greater than 0, the tweet will be sent to Slack, otherwise it will just be kept stored in the database.

### 8\. Sending positive tweets to Slack

The way to send tweets from a database to a Slack channel is via a Slackbot, which you have to create from your Slack account. Follow the instructions [on Slack](https://api.slack.com/bot-users) and in [our reference docs](https://docs.n8n.io/credentials/slack/) to learn how to create your Slackbot and get the necessary credentials (Access Token).

Once you have the Slack node credentials set up, configure the parameters:

-   *Resource*: Message
-   *Operation*: Post
-   *Channel*: YourSlackChannelName
-   *Text*: 🐦 NEW TWEET with sentiment score {{$json["score"]}} and magnitude {{$json["magnitude"]}} ⬇️\
    {{$json["text"]}}

![](https://lh3.googleusercontent.com/CU1W4OcN0xfGqQyxntlVVDEUzEndcftzYF-utzWb29pt3tGqibEyWMj7JTypmGhOJBWo3K0FVSnkd-O2-OyYhpj33705_MPo9S0sZ_NXmkDYa65Og13xf8yqbHYmjmjKC0JGghcU)


After executing the node, check your Slack channel for a new tweet:

![](https://n8n.io/blog/content/images/2021/04/Screenshot-from-2021-04-08-09-23-39.png)


### 9\. Ignoring negative tweets

The last node in this workflow is the **NoOp node**, which is used when we don't want to perform any operations. The purpose of this node is to make the workflow easier to read and understand where the data flow stops. Though this node is not necessary for our workflow, I included it to mark visually the false condition and make it clear that the workflow can be extended in this direction.

Finally, execute the whole workflow and activate it, so that it runs as scheduled. Also, check your MongoDB collection and Postgres database to make sure that the tweets have been inserted properly.

## What's next?

Congrats -- you now have an automated workflow that informs you every day about positive historical events that happened on that day! As usual, you can tweak and extend this workflow, for example by keeping track of whether a tweet has been processed already, adding an action for the condition when the IF node is false, or cleaning the text of the collected tweets to check whether it influences the sentiment score.

Of course, you can also build other ETL pipelines for various business use cases, such as product feedback at scale, Jira ticket automation based on customer sentiment, or regular database querying for reporting.