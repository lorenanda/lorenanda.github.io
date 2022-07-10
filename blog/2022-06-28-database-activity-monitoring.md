---
title: How to automate database activity monitoring and alerting
description: Learn what database activity monitoring is, why it's important, and how to automatically monitor a Postgres database containing IoT data with n8n workflows.
tags: [n8n, tutorials]
canonical-url: https://n8n.io/blog/database-activity-monitoring
---

Learn what database activity monitoring is, why it's important, and how to automatically monitor a Postgres database containing IoT data with n8n workflows.

<!--truncate-->

Database activity monitoring (DAM) is increasingly valued in organizations that work with data, as it helps ensure that mission-critical processes run optimally and issues are detected on time. Established and new companies are offering a variety of DAM tools and solutions, tailored to the needs of customers across industries.

The global DAM software market is projected to grow [by 15% by 2029](https://www.fortunebusinessinsights.com/database-monitoring-software-market-106413), with DAM tools looking to [leverage machine learning](https://www.smartdatacollective.com/database-activity-monitoring-security-investment-that-pays-off/) in their solutions. These trends are fueled largely by a sharper focus on data privacy regulations, an increased risk of cyber-attacks. In this context, DAM is a worthwhile investment.

In this article, you'll learn about database activity monitoring: what it is, how it works, why it's important, and what to monitor in your database. Moreover, you'll learn how to build an n8n workflow that automatically monitors sensor activity data in a Postgres database and sends SMS via Twilio when it detects outliers.

## What does database activity monitoring mean?

**Database activity monitoring (DAM) is the process of observing activities of a database and reporting suspicious activity.** [Gartner defines DAM](https://www.gartner.com/en/information-technology/glossary/database-activity-monitoring-dam) as "a suite of tools that can be used to support the ability to identify and report on fraudulent, illegal or other undesirable behavior, with minimal impact on user operations and productivity".

DAM tools (or workflows) can track user actions and changes made to a database continuously and in real-time, and then send notificaitions or alerts to a specified channel or person. Thus, DAM is a way of ensuring compliance in data processing, strengthening database security, and offering more visibility into database activities.

## Why is database activity monitoring important?

Essentially, database activity monitoring:

- Increases productivity and efficiency in the responsible team.
- Strengthens database security, along with data privacy and compliance.
- Helps you improve and optimize the performance of your database.
- Offers more insight into database performance and health metrics.

Especially is the context of remote work, which involves using personal devices, home connections, and maybe even unverified/insecure networks, [DAM is more important than ever](https://securityintelligence.com/posts/managed-data-activity-monitoring-dam-is-more-important-than-ever/).

## What should be monitored in a database?

**The most important issues you should monitor in a database boil down to database performance and user activity.** Specifically, these can be:

- **Suspicious user activity:** Users with admin rights (for example, database administrators or system administrators) can abuse their privileges to access sensitive data or compromise the database. Abnormal database activity can also point to bad actors inside or outside of an organization who attempt data breaches.
- **Database changes:** Whether intentional or accidental, changes to a database (for example, schema updates) can impact the performance, and it's important to review them on time.
- **Query performance:** Slow or overly complicated queries can take a long time to execute, thus decreasing performance.
- **Failures and errors:** System outages, user errors (for example, if a user accidentally deletes a row in a table), or failed queries are just some examples of situations that can (severely) impact the data and performance of a database.

## How do you monitor a database?

You can monitor a database by looking into its [**transaction logs**](https://datatechnologytoday.wordpress.com/2014/02/10/the-log-is-the-database/#:~:text=The%20database%20log%2C%20sometimes%20referred,which%20changes%20to%20the%20database.), using **DAM tools**, or setting up **workflow automations** for specific issues you want to be keep an eye on.

The process of monitoring database activity usually consists of three main steps:

1. Decide what you want to monitor in the database.
2. Set up the tool/workflow for monitoring the database.
3. Define the follow-up action to take when an issue is detected in the database.

## Tools for database activity monitoring

Nowadays, many established and new companies are offering a variety of DAM tools and solutions, tailored to the needs of customers across industries.

Here are 10 open-source and paid tools for DAM:

- **DataDog** is an enterprise observability service that provides monitoring for databases through a data analytics platform.
- **Dynatrace** is a software intelligence platform that provides database monitoring services based on artificial intelligence and automation.
- **Icinga** is an open-source computer system and network monitoring application that covers all aspects of monitoring, including database functionality and alerting.
- **ManageEngine** offers enterprise IT management software, including monitoring for both SQL and NoSQL databases.
- **NewRelic** offers cloud-based software for website and application monitoring.
- **Prometheus** is an open-source monitoring and alerting tool that allows capturing time-series data as metrics.
- **Sensu** is an open source tool that delivers monitoring as code on any cloud.
- **SigNoz** is an open-source tool for monitoring the entire software system, including the performance of database calls.
- **Site24x7** offers both free and paid monitoring services for the entire IT environment.
- **SolarWinds** offers performance and availability monitoring for websites, applications, and servers, including Database Performance Monitoring.

Another option is to use n8n for building your own custom database monitoring workflow. This way, you can take DAM one step further and send alerts to different channels, route them based on conditional logic, and integrate other popular apps or services, for example for [DevSecOps use cases](https://blog.n8n.io/devsecops-tools/).


## n8n workflow for database activity monitoring

Now that you know the basics of database activity monitoring, let's build an n8n workflow that automatically monitors a Postgres database and sends an alerts about outlier values. For this use case, we'll generate, store, and monitor sensor data (like humidity, temperature, pressure) in a Postgres database.

This automation use case consists of two workflows:

1. [**Workflow 1**](https://n8n.io/workflows/356/) generates data and creates a database record every minute. This is a way to simulate sensor readings being ingested by a database.
2. [**Workflow 2**](https://n8n.io/workflows/357/) checks for the threshold values every minute and, if a value that crosses the specified threshold, it triggers an alert with an SMS, and updates the value in the database.

### Prerequisites for building the workflow

- **n8n set up**. The easiest way is to [download the desktop app](https://docs.n8n.io/hosting/installation/desktop-app/), but you can also [sign up for n8n.cloud](https://docs.n8n.io/hosting/installation/cloud/) or [self-host n8n](https://docs.n8n.io/hosting/installation/docker/).
- **PostgreSQL set up** and [credentials](https://docs.n8n.io/integrations/credentials/postgres/). You can create the database for this workflow with the following SQL statement: `CREATE TABLE n8n (id SERIAL, sensor_id VARCHAR, value INT, time_stamp TIMESTAMP, notification BOOLEAN);`
- **Basic knowledge of SQL**. This is helpful for knowing how to create a table and query the database.

### Workflow 1 - Generate data and insert it into a database

This workflow builds the initial setup for automatic database activity monitoring. It generates sensor data and inserts the values into a Postgres database.

![workflow 1](https://blog.n8n.io/content/images/size/w1600/2022/06/dbmonitoring_workflow1.png)

The workflow consists of three nodes:

1. [**Cron node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.cron/) triggers the workflow at regular time intervals. The node has the following parameter:
   - Mode: Every Minute
2. [**Function node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.cron/) generates sensor data (sensor id (preset), a randomly generated value, timestamp, and notification (preset as false)). In the JavaScript Code field, copy-paste the following code:
   
  ```javascript
  var today = new Date();
  var date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
  var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
  var dateTime = date+' '+time;

  items[0].json.sensor_id = 'humidity01';
  items[0].json.value = Math.ceil(Math.random()*100);
  items[0].json.time_stamp = dateTime;
  items[0].json.notification = false;

  return items;
  ```

3. [**Postgres node**](https://docs.n8n.io/integrations/nodes/n8n-nodes-base.postgres/) inserts the data into a Postgres database. The node has the following parameters:
   - Operation: Insert
   - Schema: public
   - Table: n8n
   - Columns: sensor_id,value,time_stamp,notification
   - Return Fields: *

> Don’t forget to save and activate the workflow before moving on to the next workflow. Once you have done that, every minute a new record will be inserted into the database.

### Workflow 2 - Query a database and send SMS alerts

This workflow builds the actual automation for database activity monitoring and alerting. It queries the Postgres database at regular time intervals for threshold values and, if a value that crosses the specified threshold, it triggers an alert with an SMS, then updates the value in the database.

![workflow 2](https://blog.n8n.io/content/images/size/w1600/2022/06/dbmonitoring_workflow2_twilio.png)

The workflow consists of five nodes:

1. [**Cron node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.cron/) triggers the workflow every minute. The node has the following parameter:
   - Mode: Every Minute

2. [**Postgres node**](https://docs.n8n.io/integrations/nodes/n8n-nodes-base.postgres/) queries the database for values over 70 and notifications that haven't been sent (false). The node has the following parameters:
   - Operation: Execute Query
   - Query: `SELECT * FROM n8n WHERE value > 70 AND notification = false;`

3. [**Twilio node**](https://docs.n8n.io/integrations/nodes/n8n-nodes-base.twilio/) sends an SMS with information about the queried values. The node has the following parameters:
   - Resource: SMS
   - Operation: Send
   - From: phone number of the sender
   - To: phone number of the receiver
   - Message > Add Expression: `🚨 The Sensor ({{$node["Postgres"].json["sensor_id"]}}) showed a reading of {{$node["Postgres"].json["value"]}}.`

  ![twilio message](https://blog.n8n.io/content/images/2022/06/dbmonitoring_twiliomsg.jpeg)

  > You might want to turn off the other workflow or device at some point, otherwise you might end up using all your Twilio free credits during the first run.

4. [**Set node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.set/) sets the value of the notification to true for all the corresponding ids. Once you make this update in the database with the help of the next node, the SMS alerts will not go through twice for any given record. The node has the following parameters:
   - Keep Only Set: toggle to true
   - Add Value > Number:
     - Name: id
     - Value > Add Expression: `{{$node["Postgres2"].json["id"]}}`
   - Add Value > Boolean:
     - Name: notification
     - Value: toggle to true


5. [**Postgres node**](https://docs.n8n.io/integrations/nodes/n8n-nodes-base.postgres/) updates the information in the database based on the id. The node has the following parameters:
   - Operation: Update
   - Schema: public
   - Table: n8n
   - Update Key: id
   - Columns: notification
   - Return Fields: *

And that was it! Now you have two workflows that automatically monitor activity in your Postgres database and send you SMS alerts when values exceed a specific threshold.

## What's next?

In this post, you learned the basics of database activity monitoring and saw how to build a workflow that automatically monitors a Postgres database and sends SMS alerts.

Here's what you can do next:

- Read more tutorials about use cases related to databases and security, for example [How to manage database backups](https://blog.n8n.io/workflow-for-cratedb-backup-management/) or [How to automate an incident response playbook](https://blog.n8n.io/automated-incident-response-workflow/).
- Check out the [workflow page](https://n8n.io/workflows/) for more automation ideas.
- [Subscribe to our newsletter](https://n8n.io/blog/#subscribe) to get the latest news around workflow automation with n8n.
- Join the [community forum](https://community.n8n.io/) and follow us on [Twitter](https://twitter.com/n8n_io).

> This post was originally published on the [n8n blog](https://n8n.io/blog/database-activity-monitoring).