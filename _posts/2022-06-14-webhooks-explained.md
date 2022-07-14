---
layout: post
title: Webhooks explained
share-description: Learn what webhooks are, how they work, when to use them, and how to automate your workflows using the webhook nodes in n8n.
tags: [automation, n8n]
canonical_url: https://blog.n8n.io/webhooks-for-workflow-automation/
---


Since being introduced in 2007, [webhooks have revolutionized the web](https://web.archive.org/web/20180630220036/http://progrium.com/blog/2007/05/03/web-hooks-to-revolutionize-the-web/). These user-defined callbacks made it possible to access real-time data from an app, creating new infrastructure and opening up endless possibilities for web developers.

In this post, you'll learn the basics about webhooks: what they are, how they work, how they differ from APIs and polling, and when to use them. You'll also see how the [Webhook node](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.webhook/) and [Respond to Webhook node](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.respondtowebhook/) can be used to build powerful workflow automations in n8n.


## What are webhooks?

Essentially, webhooks are a way for apps to communicate with each other, kind of like keeping each other informed about updates. Webhooks are used to set instant, real-time notifications for events that take place in an app, allowing you to then take specific actions based on those events.

For example, let's say you want to send a message as soon as information gets updated in a database. The dialogue between the two apps would go like this:

– "Hey Webhook, let me know when this happens."  
– "Ok, App, I will." [a while later...] "Hey App, this thing you asked about just happened."  
– "Cool, thanks. I'll take it from here."

Think of setting a webhook like putting yourself on the waitlist for an event: the date is not set yet, so you can't sign up; you also don't want to ask every 5 minutes when it will take place, because it would be a waste of time (and very annoying); so you only ask once to be kept in the loop, then you'll just wait to receive the news.

Webhooks enable many automation and notification workflows, where it's needed to react to certain updates as they happen.

## How do webhooks work?

Now that you have a high-level understanding of webhooks, you might wonder what happens under the hood. The process can be summarized in three steps:

1. The webhook receives a request to listen to an event in System A.
2. When that event occurs in System A, the webhook makes an [HTTP POST request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) to a URL. This method asks the web server to accept the data in the body of the request message.
3. System B receives data from POST about the event that occurred in System A, and takes action. What this action is, is specified by the user.

## Webhook vs. API vs. Polling

Webhooks are not the only way to establish a communication between apps––[APIs](https://n8n.io/blog/what-are-apis-how-to-use-them-with-no-code/) and [polling](https://n8n.io/blog/creating-triggers-for-n8n-workflows-using-polling/) serve a similar purpose. However, there are some key differences between the three methods.

- **Webhooks** are event-based, as you configure them to listen to a specific event. They are also automated, so they automatically respond to an event that was set once.
- **APIs** are request-based, as you ask for a specific resource. APIs are not automated, as they give you the information only when you ask for it.
- **Polling** functions like an API, but it requests data at regular time intervals. Think of polling like the donkey in Shrek, who keeps on asking: "Do you have this info yet? How about now? But now?".

In this sense, webhooks are simpler than APIs and faster than polling.

## When to use webhooks

Knowing the difference between webhooks, APIs, and polling helps you decide when to use each method. It's best to use webhooks in the following situations:

- When you need to be informed when a specific event occurs (for example, to identify malfunctions, and act on them ASAP).
- When you need to run a workflow based on data from an app (for example, to [sync data between two systems](https://n8n.io/blog/how-to-sync-data-between-two-systems/)).
- When you need to run a workflow when an event occurs in a system (for example, to send a confirmation email when someone signs up for a course).

Webhooks are fast and efficient, as they stay alert for specific events and pass on information about them right away. So when you have a use case where these two qualities are essentials, it's a job for a webhook.

## Workflow automation with webhooks

Webhooks open up many possibilities for automating all kinds of workflows. n8n provides two nodes for working with webhooks:

- [**Webhook node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.webhook/) allows several different services to connect to n8n and run a workflow when data is received. You can use this node when there is no [trigger node](https://docs.n8n.io/integrations/trigger-nodes/) available for the app you need, or when the trigger node doesn't have the operation you need.
- [**Respond to Webhook node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.respondtowebhook/) allows you to control the response to incoming webhooks.

Here are some examples of workflows that use the (Respond to) Webhook nodes for automating various use cases, from GDPR compliance to RSS feeds.

### Automated GDPR compliance

GDPR compliance is as much an important topic, as it is a hassle to implement. Securing and deleting user can cost a team hours of tedious work. We've been there, and predictably we tried to automate at least part of this process.

This [workflow handles data deletion requests](https://n8n.io/workflows/1455) through Slack slash commands. The Webhook node triggers the workflow when the set slash command is called in Slack, and the Respond to Webhook node sends responses back to Slack.

### Automated URL shortening

URL shorteners are very useful for creating user-friendly links that can easily be shared on social platforms. However, the existing tools tend to have limited functionality.

Instead, you can use this [workflow to create a self-hosted URL shortener](https://n8n.io/workflows/1093) that also displays the number of clicks on a dashboard. Webhook nodes are used to trigger actions based on events on a specified website.

Follow [this tutorial](https://n8n.io/blog/how-to-build-a-low-code-self-hosted-url-shortener/) to learn how to set it up step-by-step.

### Automated incident response

Incidents like a server outage or data breach can cause significant damage to a business and its reputation, and it's crucial to mitigate the risks as soon as possible. In this kind of situations, workflow automation can save you precious time.

This series of three [workflows automatically follow an incident response playbook](https://n8n.io/workflows/353). Webhook nodes are used to trigger the workflows when an incident is created in PagerDuty, and when team members acknowledge and resolve the incident.

Learn more about automated incident response and how to configure the workflows step-by-step in the blog post [*How to automate every step of an incident response workflow*](https://n8n.io/blog/automated-incident-response-workflow/).

### Automated RSS feeds

What to do when you want to stay up to date with a website's content, but it doesn't provide the classic RSS feed? You guessed it, there's a workflow for that as well.

This [workflow creates an RSS feed based on a website's content](https://n8n.io/workflows/1418), using the Webhook node to trigger actions when new content is added to a specified page. The other core nodes then extract the required data and generate the feed.

### Automated reading list

Honestly, how many tabs do you keep open with articles you want to read? You haven't yet found the time, and until you do, they're there clogging your browser, staring in the back of your mind, making you feel nervous about your to-do list.

To make things easier, this [workflow automatically adds articles to Notion](https://n8n.io/workflows/1110) based on a Discord slash command. You can simply send a link in a Discord chat, and the Webhook node triggers the workflow to add that page to a Notion list.

### Automated document e-signatures

Getting a signature on a document is often the green light that allows you to move on with a project, so it's important to manage these records in a timely manner.

This [workflow manages Acrobat Sign signatures](https://n8n.io/workflows/1588), using Webhook nodes to trigger the workflow on new sign intents on a document, and the Respond to Webhook node to set the response headers.

> This post was originally published on the [n8n blog](https://blog.n8n.io/webhooks-for-workflow-automation/).