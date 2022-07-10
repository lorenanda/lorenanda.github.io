---
layout: post
title: How to automate your reading habit just in time for World Poetry Day
tags: [n8n, NLP, tutorials]
share-description: Learn how to create a no-code workflow that gets international poems, translates them into one language, and sends you a poem in Telegram every day.
canonical_url: https://n8n.io/blog/world-poetry-day-workflow/
---

March 21st is [World Poetry Day](https://www.un.org/en/observances/world-poetry-day), a day dedicated to one of the most treasured ways of expression around the world and linguistic diversity. I have always loved reading poetry with creative rhymes and melodic rhythm, and lately I have come to appreciate free verse poetry as well. In any case, I would like to make time to read more poetry and discover new international poets.

To automate this goal, I created an n8n workflow that sends a poem translated into Romanian in my Telegram chat every day. In this tutorial, I'll show you how to set it up in four steps.


## The no-code workflow

If this is your first n8n workflow, have a look at our [quickstart guide](https://docs.n8n.io/getting-started/quickstart.html) first to learn how to install n8n. Once you have your n8n Editor UI open, there are two ways to follow this tutorial: either copy the workflow from [here](https://n8n.io/workflows/975) into your Editor UI and deactivate the nodes, so that you can execute and test each node separately, or add the nodes one at a time.

![n8n Editor UI showing the workflow](https://lh4.googleusercontent.com/hK9r8CV6evcNaPzrTq-0KczIRvjbZWGDn3PDJzA1ZgnyX5DT_Gm4QR6LaK9iekbifXvLI00oq04_gdTAO12GzZz7Bp2BO7H-u_VkaP6gDE_BX2N4OH8SGdP4l7w4HLKWar-xjazP)


This workflow consists of four nodes:

1.  [**Cron node**](https://docs.n8n.io/nodes/n8n-nodes-base.cron/): triggers the workflow every day at 10:00. You can change the time and interval based on your use case.
2.  [**HTTP Request node**](https://docs.n8n.io/nodes/n8n-nodes-base.httpRequest/): makes an HTTP request to the [Poemist API](https://www.poemist.com/api/v1/randompoems) that returns random poems.
3.  [**LingvaNex node**](https://docs.n8n.io/nodes/n8n-nodes-base.lingvaNex/): translates the returned poems into Romanian. You can choose from over 100 languages.
4.  [**Telegram node**](https://docs.n8n.io/nodes/n8n-nodes-base.telegram/): posts the translated poems in the chat.

Now let's see how to set up each node.

### 1\. Schedule the workflow

First, you need to set the time and interval at which you want to receive poems in the chat. For this, set up the **Cron node**, where you can choose from seven modes and set the exact hour and minute**.** For this example, the workflow will be triggered every day at 10:00.

![n8n Editor UI showing the setting for the Cron node](https://lh6.googleusercontent.com/hNquM3fL3pJn-LnjvXBYDg2VPTWjO1KtHkmdt-WbpRIQy8w2jmCcNDhCuZ-lKtIq0VY3AABhLt8CGrcr6vruayAZ5l71-MvoE3yz6yHAFZ1RdIro89rEHlBt7b9zmQW1A8ydMNOr)


### 2\. Get poems from Poemist

Now, you need to get the poems. For this, set up the **HTTP Request node** to get data from [Poemist](https://www.poemist.com/). Paste the [Poemist URL](https://www.poemist.com/api/v1/randompoems) and execute the node to test that it's working.

![n8n Editor UI showing the setting for the HTTP Request node](https://lh3.googleusercontent.com/j09KrCZMQ53LjjtBMN1Rd6X5rWFjhLFQCFW-AcKIvxdQY_WlC7v1rLLmZUoSt9dsbzwaeUK5u_SS_2W2QfdisISJS7-b6c6JzCipNLE5I5xDqrCSEwPNJknfoie_Nr2246OFGWT9)

### 3\. Translate poems with LingvaNex

The Poemist API includes poems in different languages, which on one hand is great for linguistic diversity, but on the other hand it can be challenging if you don't know the language.

To make sure you can read all poems, translate them into a language of your choice using the **LingvaNex node**. For this, you need to sign up on [LingvaNex](https://lingvanex.com/registration/) to get credentials. You can find detailed instructions [here](https://docs.n8n.io/credentials/lingvaNex/). Copy your credentials in *LingvaNex API*, then set *Translate to* Romanian (or any other language you prefer).

![n8n Editor UI showing the setting for the LingvaNex node](https://lh5.googleusercontent.com/dzicYRHYyuKfKGcAL66sArOwXQBPUo1DfgiFobnFDMSSwM-oCun1dPNEJvQQ4M-LL2-kk0sSUasSPPY3hsZtJXgy20gh129p7aH5BLtTXmfagJOCRQv2XOaCAEHHWnE-UIrKDH05)

In the *Text* field, select:

-   The **title**: *Current Node > Input data > JSON > 0 > title*
-   The **author**: *Current Node > Input data > JSON > 0 > poet > name*
-   The **poem**: *Current Node > Input data > JSON > 0 > content*

Now execute the node to test that it's working.

![n8n Editor UI showing the expression setting for the LingvaNex node](https://lh6.googleusercontent.com/w1vkcpm0TVsFh3Jds0nNJp4kINVdSIYbTKVa2ALX6_8_mEykiUG7TDlGMy669tpFicfEQ4nvFLbOwo5Bdb6BGEJgpIJTPoQbnGGWiDrpu0myQuq3PW8itAQY2fPBpH-Op1I4s0wY)

### 4\. Send poems to Telegram

Finally, you need to send the requested poems to your Telegram chat. In your Telegram account, start a chat with [Botfather](https://telegram.me/BotFather) and follow the instructions to create a bot and get credentials. Then, go to the Telegram node and add the credentials to *Telegram API*.

Next, you need to fill in the *Chat ID* of the newly created bot. There are two ways to get your Telegram Chat ID: with the [Telegram Trigger node](https://docs.n8n.io/nodes/n8n-nodes-base.telegram/#faqs) or with a Telegram bot. You can find instructions for both methods [here](https://docs.n8n.io/credentials/telegram/).

![n8n Editor UI showing the setting for the Telegram node](https://lh6.googleusercontent.com/OmCU1qVKJ50mkimz8SZWmHaZKDKeOxzzxgLNSMI9IkeDxC8YPunmLou2XjOpgsJ0JwhKBrj6IzwRm1eQEPm9_nZiSAXo6BNyZEabbcBLWZtXXdXiS4e_OwP01Gc-fHcC5EYk9McW)

After completing the *Chat ID*, you need to set up the text you want to send to the chat. Open the *Text* field and select the poem translation from *Current node > Input Data > JSON > result*. You can add more text or emojis to prettify the message.

![n8n Editor UI showing the text field setting for the Telegram node](https://lh5.googleusercontent.com/bWPOA6V5R1sigS_FJcBwtX_3Me5_n_W0kHqFelHCwh2lFJj8dS7g2Qm5TCV6kCQpR4mXzbokNRkUMSBxNUlSmNVDBKqCzGZbZ4826Rs5Bn7qNbgWQ45_JewFWu8aboTxn5oJvScl)

Now execute the whole workflow and check your Telegram for an incoming message:

![Message of a poem in a Telegram chat](https://n8n.io/blog/content/images/2021/03/chris-montgomery-smgTvepind4-unsplash-1.jpg)

Finally, save and activate the workflow, so that it runs every day at the scheduled time.

## What's next?

That was it! Now you know how to get international poems, translate them, and send them to a Telegram chat to get your daily dose of poetry.

> This post was originally published on the [n8n blog](https://n8n.io/blog/world-poetry-day-workflow/).