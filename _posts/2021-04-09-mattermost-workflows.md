---
layout: post
title: 5 workflow automations for Mattermost that we love at n8n
tags: [automation, n8n]
share-description: Discover five of our favorite use cases of n8n with Mattermost, for both work productivity and team engagement.
canonical_url: https://n8n.io/blog/5-workflow-automations-for-mattermost-that-we-love-at-n8n/
---

[n8n](https://n8n.io/) is a fair-code licensed tool that helps you automate tasks, sync data between various sources, and react to events --- all via a visual workflow editor. Our team has been using [Mattermost](https://mattermost.com/) for internal communication since the very beginning, and in time we have developed a [ChatOps practice](https://mattermost.com/guides/chatops/) by integrating Mattermost with our workflows.

In this article, we present five of our favorite use cases of n8n with Mattermost, for both work productivity and team engagement.

### Ensure gender-inclusive language

We value diversity and want to have a workplace where each of our team members feels heard and included. To ensure this, we created a gender inclusive bot for our Mattermost channels.

If someone addresses the group as "guys" or "gals", the bot promptly replies with: "May I suggest "folks" or "y'all"? We use gender inclusive language here. 😄"

You can find this [workflow here](https://n8n.io/workflows/982) and tweak it for your team.

![gender-neutral n8n](https://mattermost.com/wp-content/uploads/2021/04/Gender-neutral-n8n.webp "Gender inclusive")

## Schedule coffee chats

Since we started working from home, we miss having spontaneous chats over a cup of coffee in the office kitchen. But we found a way to keep this habit and catch up with the team even remotely.

We created a workflow that runs every Monday morning, randomly divides the members of a Mattermost channel into groups, announces the pairs in the chat, and creates an appointment for a coffee chat in each person's calendar.

Read our [blog post](https://n8n.io/blog/how-to-host-virtual-coffee-breaks-with-n8n/) to learn how to set up this workflow for your team.

## Track Twitter mentions

We love to see how people all over the world use n8n for creative workflows. Many users share their workflows on Twitter and we want to keep track of these mentions, so that our team gets inspired and knows how to improve the product.

To this end, we created a workflow that searches for tweets that mention @n8n_io and posts them into a dedicated Mattermost channel every minute.

Read our [blog post](https://n8n.io/blog/creating-triggers-for-n8n-workflows-using-polling/) to learn how to set up this workflow for yourself.

## Announce version releases

We are continuously improving our product and regularly release new versions.

In order to keep everyone up to date with the latest changes, we automated the announcement of n8n version releases in Mattermost. When a new version is created, it triggers a workflow, which posts the version update in the channel. From here, one of our developers can push the new version to staging or production on n8n.cloud with a click directly in the chat window.

Announcements like these put a smile on our face!

## Custom slash commands

Mattermost provides [slash commands](https://docs.mattermost.com/developer/slash-commands.html), which are useful for performing operations quickly by simply typing a word. On top of the basic ones, we created several custom slash commands integrated with n8n workflows for different purposes.

### /brand command

The `/brand` command returns n8n's brand assets --- like our brand color, icon and logo, marketing copy, and useful administrative links. This slash command is especially useful to the Design and Marketing teams, when in need of a quick reference.

### /call command

Sometimes, we need to hop on a call spontaneously to discuss or clarify some things. We use Whereby for ad-hoc meetings, and to make the call setup process even easier, we created a custom Mattermost slash command `/call.`

When someone invokes it, it posts their Whereby URL in the Mattermost channel with the message: "Please join a call with me at: [Whereby-URL]".

Read our [blog post](https://n8n.io/blog/the-ultimate-guide-to-automate-your-video-collaboration-with-whereby-mattermost-and-n8n/) to learn how to set up this workflow for your team.


### /devrel command

Our DevRel team handles many projects in parallel, from the documentation and blog posts to user interviews and community engagement. Naturally, various questions about content or technical details arise.

To get help, we created the slash command `/devrel`, which returns a link to a request form where team members can describe their issue or question, which is then converted into a Jira ticket for the team.


### /docs command

Our developers and technical writers are constantly writing and updating the documentation of n8n nodes. To help them keep track of the documentation status, we created the slash command `/docs`, which returns the number of undocumented nodes and the current coverage of the documentation in the Mattermost channel.


### /graphic command

Almost every week, we make a release of n8n with new nodes, features, or improvements, and share the news on our social media channels along with an image. This image used to be created manually by someone in our team --- a repetitive task that could easily be automated.

For that, we created a custom slash command `/graphic` that only requires the version number and links to the logos of the new nodes, and then outputs the release graphic directly into the chat window.

This workflow is particularly helpful for design and marketing teams.


## Conclusion

To sum up, we showed you five different n8n workflows used with Mattermost that make our lives easier and team happier. n8n's open ecosystem of integrations allows you to connect and incorporate Mattermost with your favorite services and products to create a unified automation workflow for a wide range of use cases.

> This post was originally published on the [Mattermost blog](https://mattermost.com/blog/5-workflow-automations-for-mattermost-that-we-love-at-n8n/).