---
layout: post
title: 15 Google apps you can combine and automate to increase productivity
tags: [tutorial, n8n]
share-description: Learn how to combine and automate popular Google apps for more productivity in the workplace.
canonical_url: https://n8n.io/blog/automate-google-apps-for-productivity/
---

Google creates some of the best services on the web for professional use cases, with G Suite being the go-to choice for many businesses. One of the  main advantages is having an ecosystem of apps for various specific uses: from organisation and productivity tools to databases and language processing services.

[n8n](https://n8n.io) offers **15** [**nodes**](https://n8n.io/integrations/)for the most popular Google apps that you can combine to build powerful automated workflows. In this article, we'll give you some ideas of processes you can automate, so that you can boost productivity in the workplace, save time from repetitive tasks, and focus on what matters.

![](https://lh4.googleusercontent.com/mue5xS4vtJDh6uiinkOvHQzdBKF5WbCdvFW-HnFlZ6WUM4Hfxk4ffcJ18osdXjEZWC_tOHLsNDCsjgCCq03HdINLlJrFFroVt4b6gBexoT4p54fm7S4Slfkynuhk4VfP9vFllolx)


Specifically, we'll show you **six workflows** that use various Google nodes to automate analytics reports, database monitoring, onboarding processes, event registrations, feedback analysis, and file management--there's something for everyone!

## Connect Google Analytics and BigQuery to Sheets and Gmail to automate your reports

To meet your business goals and check whether you're on the right track, it's important to keep an eye on different metrics (like visitors to your website, the performance of online campaigns) and create regular reports for stakeholders or clients. These tasks can be repetitive, so why not let [this ready-made workflow](https://n8n.io/workflows/892) do the work for you? The [**Google Analytics** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleAnalytics/) will get the number of sessions on your website, grouped by country, and store the data in Airtable (or in [**Google Sheets**](https://docs.n8n.io/nodes/n8n-nodes-base.googleSheets/), to stay in the Google ecosystem).

![](https://lh6.googleusercontent.com/OyQDv3Zwqsmg8CdLILFnJbdDNa_xYdNK5p9MYkSZro0aOhQn4qDxzDNhQ5C_sidZLtffA1hDJoi5tNcbcgeox5bluRufCu5_zOJs7qY2N81Wc509qgTDoAkIZj4SCNTrI3vCtq5g)


You can further extend this workflow by adding a [**Gmail** node](https://docs.n8n.io/nodes/n8n-nodes-base.gmail/) that emails the report to the stakeholders, so that you save up another 5 precious minutes of your work day! In addition, you can add a [**Google BigQuery** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleBigQuery/)to retrieve records from or insert new records into your data warehouse. And if you're feeling particularly creative, you can even create a dashboard for KPIs from different sources, as explained in [this tutorial](https://n8n.io/blog/automatically-pulling-and-visualizing-data-with-n8n/).

## Connect to Google Cloud Firestore to automatically monitor your databases

Another common use case related to data management is database monitoring, where you need to track the performance of your database and monitor key metrics in real-time, to quickly identify and fix potential issues. Google offers two cloud-based databases for real-time data syncing: Cloud Firestore and Realtime Database; n8n offers you the nodes to automate them: [**Google Cloud Firestore** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleFirebaseCloudFirestore/#basic-operations) and [**Google Cloud Realtime Database** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleFirebaseRealtimeDatabase/). You can schedule workflows like [this one](https://n8n.io/workflows/787) that regularly inserts data into a database or updates it.

![](https://lh5.googleusercontent.com/FmAPPVq8Il79qdql-rymOmvkWNNc8H3Ag9__iBEC_gAvxI-XmrbULX-Fh4aB2opeoBbIwjw_AO75JhCJYD3be9JDaLOyadVocbWZAPaA6Ek8dhTizAfFH1XmmMGMLCLEVjqGHbyw)

## Connect G Suite apps to automate the onboarding of new team members

Hiring new members for your team is an exciting moment! Not so exciting is the series of small boring tasks you need to do in advance, like creating an email account and setting up meetings. You can turn this process into an automated workflow that uses the [**Gmail** node](https://docs.n8n.io/nodes/n8n-nodes-base.gmail/) to detect when you get an email with the subject "Welcome our new team member!", then [creates a new user account](https://n8n.io/workflows/710) with the [**G Suite Admin** node](https://docs.n8n.io/nodes/n8n-nodes-base.gSuiteAdmin/), [adds the user to your contacts](https://n8n.io/workflows/637) using the [**Google Contacts** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleContacts/), and finally schedules a welcome meeting for you using the [**Google Calendar** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleCalendar/). Now your new hire is all set up for their first day and you have more time to prepare a nice onboarding experience (you could even let the [**Google Tasks** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleTasks/) add that to your to-do list automatically).

## Connect Typeform to Google Sheets and Calendar to automate event registrations

Organising an event involves a lot of work, even in these times when most of them are hosted online. One of the main challenges is keeping track of attendees and notifying them on time about the latest updates in the program. Doing these things manually would be not only time-consuming, but also prone to error. Luckily, this too can be automated and we even have an [in-depth tutorial](https://n8n.io/blog/supercharging-your-conference-registration-process-with-n8n/) dedicated to this use case. The workflow makes use of the [**Google Sheets** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleSheets/) to store information from a registration form like [Typeform](https://www.typeform.com/), the [**Google Calendar** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleCalendar/) to create events for the conference sessions, and the [**Gmail** node](https://docs.n8n.io/nodes/n8n-nodes-base.gmail/) to notify the attendees. For more engagement, you can use the [**Orbit** node](https://docs.n8n.io/nodes/n8n-nodes-base.orbit/) to pull in community metrics or post notifications.

![](https://lh3.googleusercontent.com/NnGUrPUi8kYmXY3S4ccoPlNPpzRnHhQ7FwuF0EymJy6jfpU7Dc5ilwiyOJyN1U4jz_crrc0E7jHC8rbkVvS5JHr-3KV6Tfe7aZEMsIeCim6_yIC1eVoJVlzt_st1XA48747snOMq)


## Connect Typeform with Google Natural Language and Sheets to analyse and store customer feedback

Getting feedback on your product or service is an incredible opportunity for improvement. Particularly insightful are written reviews from customers, but simply reading them is not feasible, especially as your customer base grows. A [workflow for this case](https://n8n.io/workflows/1075) uses [**Google Cloud Natural Language** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleCloudNaturalLanguage/) to analyse the sentiment of reviews submitted in Typeform, filter positive and negative reviews, and store them in [**Google Sheets**](https://docs.n8n.io/nodes/n8n-nodes-base.googleSheets/). Depending on your needs, you can also translate the reviews with the [**Google Translate** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleTranslate/) before analysing them.

![](https://lh3.googleusercontent.com/dpa4aF88iDaKpH3hKZbwsZ3JGgCteqe4ewFKrW47NUevxOy36CeNgJnrrf_cdby-G326Ew_piSuHOprxe5rcaRCct76oIGMp3F9R1K0SZIroNmrtHPo_iQhbJ95ABUbgvubVSzdN)

## Connect Google Drive to Slides and Gmail to automatically manage your files

Let's face it: we could all be a bit tidier in our digital workspace. But it seems like no matter how rigorously you organise your folders, a document always gets saved mistakenly in the wrong folder and before you know, digital clutter reigns.

A solution to this problem is automating the regular file flow, so you don't have to worry about it anymore. For example, you can start with [this workflow](https://n8n.io/workflows/1035) to get the [**Google Slides**](https://docs.n8n.io/nodes/n8n-nodes-base.googleSlides/) of your weekly presentation, add the [**Google Drive** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleDrive/) to store the slides in a shared team folder and the [**Gmail** node](https://docs.n8n.io/nodes/n8n-nodes-base.gmail/) to email them to the team members.

You can also connect the [**Google Drive** node](https://docs.n8n.io/nodes/n8n-nodes-base.googleDrive/) with other apps to automatically save files sent to you in a specific folder. Even your personal budget can be automated, as you can learn from [this tutorial](https://n8n.io/blog/automatically-adding-expense-receipts-to-google-sheets-with-telegram-mindee-twilio-and-n8n/) that shows you step-by-step how to add your expense receipts to [**Google Sheets**](https://docs.n8n.io/nodes/n8n-nodes-base.googleSheets/).