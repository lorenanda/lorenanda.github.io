---
layout: post
title: 5 tasks you can automate with the new Notion API
tags: [n8n]
share-description: Notion's API opens new possibilities. Discover what workflows you can automate now!
canonical_url: https://n8n.io/blog/5-tasks-you-can-automate-with-notion-api/
---

If you're into productivity and organisation hacks, you've probably heard of (and even got to love) [Notion](https://www.notion.so/), the all-in-one workspace app that allows you to take notes, create databases, manage projects, and schedule tasks--all with highly customisable designs.

At n8n, we've been using Notion since day one for the internal organisation: from meeting notes and onboarding checklists to content calendars and product research. Imagine our excitement when we heard that [Notion launched their API (beta)](https://developers.notion.com/), thus opening new possibilities of using the app in a more personalised way!


Our developers got to work right away and [we launched](https://www.producthunt.com/posts/notion-n8n-integration) two of the most awaited nodes: [**Notion node**](https://docs.n8n.io/nodes/n8n-nodes-base.notion/#basic-operations) and [**Notion Trigger node**](https://docs.n8n.io/nodes/n8n-nodes-base.notionTrigger/).

The **Notion node** has five basic operations that allow you to manage blocks, get and query databases, create and update records in a database, create and search for pages, and get users who are part of your workspace. The **Notion Trigger node** allows you to check at regular intervals when a page is added to the database, then trigger a workflow.

Now you can easily connect your tools to Notion to sync data and boost your productivity. We're super excited to automate some of our workflows, and even more so to see what other creative ideas the [n8n community](http://community.n8n.io/) comes up with. In this article, we'll present to you **5 Notion workflows** you can automate in n8n:


## Add candidates' profile assessment to Notion before an interview

Scheduling interviews has become easier thanks to apps like Calendly, but evaluating candidates' skills and personality still requires a human touch and good psychological understanding. [Humantic AI](https://humantic.ai) can complement recruiters' evaluation, by generating psychometric assessments (including [DISC](https://en.wikipedia.org/wiki/DISC_assessment) and the [Big Five personality traits](https://en.wikipedia.org/wiki/Big_Five_personality_traits)) from candidates' résumés.

For this use case, we created [a workflow](https://n8n.io/workflows/1107) that is triggered when an interview is scheduled via Calendly. The Humantic AI node retrieves the LinkedIn profile of the candidate from Calendly, creates their psychometric assessment, then the Notion node inserts this information into a dedicated page.

By automating this process, you don't have to worry about your applicant database being up to date, and instead, you have more time to prepare for the meeting.

![](https://lh3.googleusercontent.com/eam2Ikgu4aGqo6mcnDKyq3viUjLGH5zs9XA-p2_5gIroCFtZ4GCTFYmHK79PtTjEplv4GyaZwB8WlfZn-vL64uNLO1h9JbL9ImDb8Y_vprrNJdFyv3vbLaOno_5hhJ3jHURhO_aY)


## Check to-do's in Notion and notify the assignee in Slack

One of the most useful applications of Notion for teams is keeping to-do lists where you can assign tasks to specific people. A limitation is that the in-app or email notifications can easily be overseen and are out of context. To overcome this issue, you can use [this workflow](https://n8n.io/workflows/1105) that regularly checks your to-do list in Notion and notifies the person in Slack when a new task is assigned to them.

![Workflow for to-do list notification](https://lh5.googleusercontent.com/cYTvsnlN0p8PbiuPd7DTC2Ravaw8WB9U4m9NIKNA2dRKlQZtHH9X77DBFasfLLhIDJXtHbY9yHVHB52MMnVmVY9IDNgWJRGunpAcX-qwRTbx3DxJMHOir6IFxe3cSnR2A1tPI6n5)


Of course, you can replace the Slack node with another messaging app of your choice. We prefer Mattermost and have built several [workflows around it](https://n8n.io/blog/5-workflow-automations-for-mattermost-that-we-love-at-n8n/), which substantially improve our communication and productivity.

## Send notifications about new Notion notes to Mattermost

Another practical use of Notion pages is for taking notes in meetings and keeping them well-organised by topic or meeting type. After the meeting, you might first want to go get a coffee before taking care of the action items just discussed. But as it often happens, even a short break can interrupt your working flow, so you may easily forget what you needed to do or who you had to follow up with once you're back at your desk.

Luckily, you can automate your chores away! [This workflow](https://n8n.io/workflows/1089) is triggered whenever new meeting notes are added in Notion. If the property field in the notes mentions the Marketing team, a message about the new notes will be sent to the Marketing channel in Mattermost, so all team members are up to date. Now you can enjoy your long-awaited coffee break knowing that the main action items will be taken care of.

![Workflow for meeting notes updates](https://lh6.googleusercontent.com/tlVM2zUetq3H-9LuD930xgz42RQqWGQvd-JxKCQIf6P1s4oAEYLopnfZASlmk0ySFhxMgcp6FoVLfS4uZPEqrcbAerLXvYKnNT2kVSMSDNQQ8nHbYmNt6pR1y23Mk-BZq4m71Zwm)


## Add positive feedback messages to a compliments table in Notion

We, humans, are prone to [negativity bias](https://en.wikipedia.org/wiki/Negativity_bias), meaning that we remember negative experiences more (strongly) than positive ones. For example, in a business context, when getting feedback from customers on your product or service, you are more likely to keep in mind that one negative review over the other tens of praise messages. This bias can impact your perception of your work and the team spirit, so it's important to highlight the good news.

For this use case, we built [a workflow](https://n8n.io/workflows/1109) that analyses the sentiment of feedback messages submitted via Typeform: messages with negative sentiment are added to a Trello board, while the ones with positive sentiment are added to a compliments table in Notion, then shared in a Slack channel. Looking once in a while at the impact you have on your customers is a wonderful way to keep your team motivated and inspired!

![Workflow for feedback message analysis](https://lh6.googleusercontent.com/-z6QPNwDy4xAVe8u865TD9-Ba03wL4LMN4uj6BcRzNqZR92bwkK960oBEhVUcv6j3HEpjhH3Fo8v4L4QwLGvOQxulSRZeQ6FyX6EsnUSq1V9vKtBne8lwapynnH7mMI_vYYJHdwd)

## Add memorable articles to your Notion reading list

The modern day reading list includes more than just books. [Millions of blog posts](https://wordpress.com/activity/posting/), news articles, and research papers are published every day, serving you information on how to solve problems, improve various skills, make informed decisions--or are just food for thought. You'll most probably stumble on some articles worth sharing or saving for a later (re-)read.

To help you manage your reading list, we designed [a workflow](https://n8n.io/workflows/1110) that automatically adds important articles to a Notion page from Discord. When you type in [Discord the slash command](https://discord.com/developers/docs/interactions/slash-commands) `/[URL]`, with the URL of the article you want to save, the workflow extracts the article title and adds the linked title to the reading list in your Notion page. When all is done, you get a confirmation message on Discord: "The link was added to Notion." Now you can focus only on reading and taking notes.

![Workflow for reading list management](https://lh5.googleusercontent.com/zy2CR3lyQClhHD8itnQjc1pTOApsKRH7LSqo-N63M8Z0xVE0yw6wHfSYs192NQr_GSwccSHykfqS9UTphbh8m145THKxvvq9nRr6GKxBX0w9JyyPsXU6ndmerBhy31db_VDlj0Mw)

> This post was originally published on the [n8n blog](https://n8n.io/blog/5-tasks-you-can-automate-with-notion-api/).