---
layout: post
title: 7 no-code workflow automations for Amazon Web Services
tags: [automation, n8n]
share-description: Discover what and how AWS integrations can help you automate tasks like managing receipts, transcribing audio files, or sending localized emails.
canonical_url: https://blog.n8n.io/aws-workflow-automation/
---

Cloud computing has significantly changed the way companies operate. The option of using networks of remote servers hosted on the internet to store, manage, and process data enables organizations to scale and accelerate their digital transformation. The [leading cloud infrastructure service provider](https://www.statista.com/chart/18819/worldwide-market-share-of-leading-cloud-infrastructure-service-providers/) is Amazon Web Services (AWS), which covers [more than half](https://www.statista.com/statistics/1202770/hyperscaler-iaas-paas-market-share/) of the global hyper-scale cloud market of Infrastructure as a service (Iaas) and Platform as a Service (PaaS). 

AWS products range from data storage and networking to machine learning applications, offering solutions for pretty much every business domain. For all the functionality, it can be complicated to manage data between AWS and other services that are usually needed for a complete application. This process typically relies on either manual transfers or technical solutions, which are often complex to set up and unmanageable by users outside the engineering team.

This is where no-code workflow automation comes in: with n8n’s **11 AWS nodes** (AWS Comprehend, AWS DynamoDB, AWS Lambda, AWS Rekognition, AWS S3, AWS SES, AWS SNS & AWS SNS Trigger, AWS SQS, AWS Textract, and AWS Transcribe), you can build workflows that automate mission-critical processes in your organization and provide an overview of your workflow orchestration in a single application. In this article, we’ll show you 7 workflow automations using AWS integrations that you can copy-paste to implement in your business.


## Analyze text sentiment with AWS Comprehend

The Natural language processing (NLP) market is [forecast to increase](https://www.statista.com/statistics/607891/worldwide-natural-language-processing-market-revenues/) rapidly in the next few years, with more and more businesses adopting NLP applications to derive insights from speech and text. The AWS Comprehend node uses Amazon’s NLP service, which allows you to analyze the sentiment of a text and identify the dominant language in which the text is written. These functions are particularly useful for analyzing reviews or feedback messages at scale.

For example, if you ask your clients for feedback via Typeform, you would want to know immediately if there was a negative response. This [workflow that analyzes feedback sentiment](https://n8n.io/workflows/965) allows you to do that automatically! It analyzes the sentiment of the responses as soon as they are submitted, and you can send negative responses to a Mattermost (or Slack) channel, to be handled by your customer service team.

## Sync data between AWS S3 and Google Drive

[By 2025](https://cybersecurityventures.com/the-world-will-store-200-zettabytes-of-data-by-2025/), around 100 zettabytes of data will be stored in the cloud. [As of 2021](https://www.statista.com/statistics/1062879/worldwide-cloud-storage-of-corporate-data/) already, companies store around 50% of all corporate data in the cloud, as a measure to improve security, reliability, and business agility.

n8n provides nodes for the [most popular storage services](https://www.statista.com/statistics/1258456/enterprise-data-storage-software-market-share-vendor-worldwide/) like AWS S3, Google Drive, and Dropbox, which allow you to create buckets or folders, upload and download files, and manage users. This [Google Drive & AWS sync workflow](https://n8n.io/workflows/1396) lets you sync files one-way (or two-ways) between Google Drive and AWS S3 so that, whenever a file is updated in Google Drive, it is automatically updated in S3 as well. This way, you can rest assured that your data is up-to-date and doesn’t get lost or wrongly overwritten, and it only takes a few minutes to set up 

## Extract text from receipts or invoices with AWS Textract

An [emburse report](https://www.emburse.com/assets/pdfs/21.emb.dem_trendsreport_report-fa.pdf) found that 29% of organizations rely on manual processes and spreadsheets for managing expenses, and 67% need up to one week to process expense reports–slowing down the overall business. It comes as no surprise then that automation is the most valued solution, particularly for mobile receipt capture.

With this [text-extraction workflow for Telegram](https://n8n.io/workflows/1393), you only need to send a photo of your receipt in a Telegram channel; from there, the AWS Textract node extracts the text from the photo (like vendor and price), then this information is stored in Airtable for analysis. For a nicer user experience, you can take this workflow a step further and build an expense-tracking app.

## Transcribe cloud-stored audio files with AWS Transcribe

Unlike written text, audio data can’t be searched and analyzed by computers. This makes it more difficult to analyze and derive insights from sources like customer service calls, speeches, or presentations, or repurpose this content. A solution to this problem comes from Amazon Transcribe, which uses automatic speech recognition to convert speech to text.

The AWS Transcribe node can create, delete, and get transcription jobs for audio or video files. For the use case mentioned above, we created a [workflow that automatically transcribes audio files](https://n8n.io/workflows/1394) uploaded to Google Drive, and stores the recording information and transcript in Google Sheets.

## Label images with AWS Rekognition

Computer vision technologies like AWS Rekognition can be [used across industries](https://www.amazon.science/latest-news/how-some-of-awss-most-innovative-customers-are-using-computer-vision-technologies), for example, to classify traffic signs for autonomous vehicles, verify a person’s identity with facial recognition, and even detect skin cancer.

With the AWS Rekognition node, you can automate the process of identifying faces, labels, and celebrities in images. If you already have a collection of images, you can tweak the previous workflow and replace the AWS Transcribe node with the AWS Rekognition node.

If you don’t, you can use this [image collection & annotation workflow](https://n8n.io/workflows/1401) to search for images on a specific query (for example, with Google’s Custom Search API), detect labels in them, and store this information in a Google Sheet to serve as a data set for training machine learning models. This way, you can save your team hours of manually collecting and labeling images, and drastically cut the costs associated with these tasks.

## Email screenshots with AWS SES

Amazon Simple Email Service (SES) aims to help digital marketers and application developers send transactional emails easier. The AWS SES node allows you to send emails and manage templates and custom verification emails from within any application.

For example, you can include this node in a [workflow that automatically takes screenshots](https://n8n.io/workflows/857) of a specified website, saves them to Dropbox, and emails them to responsible team members. With this automation, you can save precious time on tedious tasks and instead focus on your business ideas.

## Send localized emails with AWS SES

Another use case for AWS SES is email localization, which means adapting your text to readers who speak different languages or live in different countries. [60% of global consumers](https://www.shutterstock.com/blog/infographic-global-localization-stats) rarely or never buy from English-only websites; as a result, 80% of marketers consider content localization essential for entering new markets, and 71% attribute increased sales to their localization strategy. In short, to effectively reach your target customers, you should invest in proper localization.

Here’s a quick idea to start optimizing your email marketing campaign: this [marketing email localization workflow](https://n8n.io/workflows/851) detects your web visitors’ countries by IP address and, depending on the region, sends the users an email in English or Spanish. You can tweak the workflow to make an even finer distinction between European and Latin American Spanish, for example, and adjust your text accordingly. With a few clicks, this automation can improve customer experience and engagement.

## Start automating!
In this post, we showed you seven workflow ideas for automating for AWS tasks. Using the linked templates, it should only take a few minutes to set up each workflow. It’s a minor time investment with major benefits: saving up hours of tedious manual work,  increasing conversion rates, improving customer experience, solidifying data processing pipelines, and speeding up business insights.


> This post was originally published on the [n8n blog](https://blog.n8n.io/aws-workflow-automation/).