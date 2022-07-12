---
title: How to automatically import JSON into Google Sheets
description: Discover three ways to import JSON data into Google Sheets or a CSV file, and five no-code workflows for automating these tasks.
tags: [n8n, tutorials]
canonical-url: https://blog.n8n.io/google-sheets-import-json/
---


[JavaScript Object Notation (JSON)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON) is a standard text-based format that is used to store and represent structured data. JSON is commonly used in web applications, and is one of the most popular [API](https://blog.n8n.io/what-are-apis-how-to-use-them-with-no-code/) formats.

Data in JSON format is not practical if you want to share that data in a user-friendly form, or perform data analysis on a data set. Most commonly, you'll need to import JSON into a spreadsheet.

In this post, we'll show you three ways to import JSON data into Google Sheets or a CSV file, and five no-code workflows for automating these tasks.

## How to get data from JSON to Google Sheets?

There are different ways to import JSON data into Google Sheets. You can use:

- Custom code
- Apps Script
- No-code tools

### Using custom code

You can write code in your preferred programming language to parse JSON data. This offers you freedom, flexibility, and control over your script. For example, you can extract certain data points and perform data analysis, along with transferring it into Google Sheets. The downside is that, depending on the use case, writing a custom script can be overly complicated.

For example, if Python is your go-to language, you can follow [this quickstart guide](https://developers.google.com/sheets/api/quickstart/python) for creating a command-line application that makes requests to the Google Sheets API, or use [this Python script](https://www.geeksforgeeks.org/convert-json-to-csv-in-python/) to export JSON data into a CSV file.

### Using Apps Script

[**Apps Script**](https://developers.google.com/apps-script) is the cloud-based JavaScript platform from Google. With Apps Script, you can integrate with and automate tasks across Google products. For example, you can create your own `=IMPORTJSON()` formula for Google Sheets to parse JSON data. However, this use is limited to the Google ecosystem, plus you need to know how to code in JavaScript.

Here's **how to use a script in Google Sheets**:

1. In your Google Sheet, select Extensions > Apps Script.  
  This opens a new untitled project in Apps Script in your browser. The project includes a place-holder function in the code editor.
2. In the code editor, replace the place-holder function with the code for creating a function to import JSON. For example, you can use [this public script](https://gist.github.com/paulgambill/cacd19da95a1421d3164).
3. Save the project under a descriptive name, for example *Import JSON*.
   Now you can use this function as a custom formula in Google Sheets.
4. In Google Sheets, select a cell where you want to import JSON data, and type the formula you created `=IMPORTJSON()`.

### Using no-code tools

No-code tools, such as n8n, require no coding skills. Compared to the previous two options, no-code tools are easier to use, yet allow you to build complex workflow automations. You can use [core nodes](https://docs.n8n.io/integrations/core-nodes/) for getting data from an API and converting data between binary and JSON format, and [integrations](https://n8n.io/integrations/) for transferring the data between apps and services, such as Google Sheets or Gmail.

## No-code n8n workflows to import JSON to Google Sheets

In the following sections, we'll show you NUMBER workflows for importing JSON data into Google Sheets and CSV files, and the other way around. You can copy-paste these workflows and make minor changes to implement them for your use cases.

**Prerequisites for building the workflows**

- [**n8n set up**](https://n8n.io/pricing). The easiest way to get started is to [download the free desktop app](https://docs.n8n.io/hosting/installation/desktop-app/), but you can also [sign up for n8n Cloud](https://docs.n8n.io/hosting/installation/cloud/) or [self-host n8n](https://docs.n8n.io/hosting/installation/docker/).
- **A Google account and [credentials](https://docs.n8n.io/integrations/credentials/google/)**. You need these to use the [Google Sheets integration](https://n8n.io/integrations/18-google-sheets-/) to access the Google Sheets API. The API is free to use, but beware of rate limits.
- Basic understanding of **APIs and JSON**. This would help you understand how to make GET requests and interpret data in JSON format.

### Workflow to import JSON from an API into Google Sheets

[This workflow](https://app.n8n.io/workflows/1737) gets data from an API and stores it into Google Sheets. Feel free to copy-paste the workflow in your n8n editor, and continue reading the instructions to understand how it works and how you can tweak it.

![workflow](./blog_images/importjson_workflow_apisheetscsv.png)

The workflow consists of three nodes:

1. [**HTTP Request node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.httprequest/) makes a GET request to the [Random User API](https://randomuser.me/api/).

  If you access the API link in your browser, you should get information about a fictional person in JSON format, which looks like this:

  ```
  {"results":[{"gender":"male","name":{"title":"Mr","first":"Giorgio","last":"Jeuring"},"location":{"street":{"number":9927,"name":"Beckershagen"},"city":"Winneweer","state":"Drenthe","country":"Netherlands","postcode":59748,"coordinates":{"latitude":"47.5171","longitude":"-140.6882"},"timezone":{"offset":"-6:00","description":"Central Time (US & Canada), Mexico City"}},"email":"giorgio.jeuring@example.com","login":{"uuid":"553f1f08-61d6-48fc-b9d7-5f21f844f0ce","username":"ticklishladybug384","password":"mondeo","salt":"yfYyG0YB","md5":"7f53e13d5002fbc2005bea41767dc68e","sha1":"255e2838819b92038ba4ccb04a38f2aa93aba868","sha256":"5a3532ccc6fb3bde566b5e38023a509cefdd0fa9214508ac08141c7e759677dc"},"dob":{"date":"1997-01-01T03:37:12.559Z","age":26},"registered":{"date":"2004-08-28T03:29:17.926Z","age":18},"phone":"(952)-290-7836","cell":"(367)-506-5505","id":{"name":"BSN","value":"65540109"},"picture":{"large":"https://randomuser.me/api/portraits/men/10.jpg","medium":"https://randomuser.me/api/portraits/med/men/10.jpg","thumbnail":"https://randomuser.me/api/portraits/thumb/men/10.jpg"},"nat":"NL"}],"info":{"seed":"6176dc854625bdf5","results":1,"page":1,"version":"1.3"}}
  ```

  In the n8n workflow, the execution of the HTTP Request node returns the result like this:

  ![http request node result](./blog_images/importjson_httprequestnode.png)

  This result includes a lot of information, but you probably don't need all of it, and want to save only the person's name and country.

2. [**Set node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.set/) sets the values you want to store from all the data you get from the API. In this case, it sets values for the name and country of the fictional person.

  ![set node result](./blog_images/importjson_setnode.png)

  This is the data that you have to store in Google Sheets.

3. [**Google Sheets node**](https://docs.n8n.io/integrations/nodes/n8n-nodes-base.googlesheets/) appends the set data to a sheet.  
   Before executing the node, go to the sheet you want to import data into and create two columns with the names of the values set in the Set node (*name* and *country*). Then, when you execute the node, you should see the name and country data being filled in under the column names in the sheet.

### Workflow to export JSON data from an API to a local CSV file

Instead of (or in addition to) importing JSON data into Google Sheets, you can  export the data to a local CSV file. To do this, you need to replace the Google Sheets node with the Spreadsheet File node (or connect a Spreadsheet File node to the Set node, if you want to save data in both Google Sheets and a local CSV).

When you execute the Spreadsheet node, it should return a CSV file that you can view and download.

![spreadsheet node](./blog_images/importjson_spreadsheetnode.png)

### Workflow to convert a CSV file to a JSON file

[This workflow](https://app.n8n.io/workflows/1732) converts a local CSV file to a JSON file. The catch here is to convert the data from JSON (the format in which the contents of the CSV file are returned) to binary (the format in which the JSON file is written).

![workflow](./blog_images/importjson_workflow_csvfilejsonfile.png)

1. [**Read Binary File node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.readbinaryfile/) reads the local CSV file.
2. [**Spreadsheet File node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.spreadsheetfile/) reads the content of the CSV file.
3. [**Move Binary Data node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.movebinarydata/) converts the data from JSON to binary format.
4. [**Write Binary Data node**](https://docs.n8n.io/integrations/core-nodes/n8n-nodes-base.writebinarydata/) creates a JSON file that contains the informations from the original CSV file. You can then download the JSON file locally.

### Workflow to import a local JSON file into Google Sheets

For this example, you can copy the JSON code from the HTTP Request node and paste it in a local json file named `users.json`.

```json
{
  "results": [
    {
      "gender": "male",
      "name": {
        "title": "Mr",
        "first": "Daniel",
        "last": "Young"
      },
      "location": {
        "street": {
          "number": 4689,
          "name": "Vimy St"
        },
        "city": "Woodstock",
        "state": "Prince Edward Island",
        "country": "Canada",
        "postcode": "R6Q 7U7",
        "coordinates": {
          "latitude": "-60.5814",
          "longitude": "-131.6670"
        },
        "timezone": {
          "offset": "+10:00",
          "description": "Eastern Australia, Guam, Vladivostok"
        }
      },
      "email": "daniel.young@example.com",
      "login": {
        "uuid": "3ff7efb9-fdd1-42cd-b669-0d737530ad5f",
        "username": "happymeercat108",
        "password": "gofast",
        "salt": "91ZgiW1o",
        "md5": "9181752b52eca6ba4024a809506963d3",
        "sha1": "35874f1666924b9f90403852154bbb3a4b5c784c",
        "sha256": "8af1b73aed0890c75d76501317bdcda58cd8d82d3090f5fbbe88c4f34a0a24e8"
      },
      "dob": {
        "date": "1991-09-16T14:12:51.147Z",
        "age": 31
      },
      "registered": {
        "date": "2010-09-10T04:22:34.603Z",
        "age": 12
      },
      "phone": "431-068-3900",
      "cell": "761-641-1531",
      "id": {
        "name": "",
        "value": null
      },
      "picture": {
        "large": "https://randomuser.me/api/portraits/men/24.jpg",
        "medium": "https://randomuser.me/api/portraits/med/men/24.jpg",
        "thumbnail": "https://randomuser.me/api/portraits/thumb/men/24.jpg"
      },
      "nat": "CA"
    }
  ],
  "info": {
    "seed": "a18f2fe366e8b0f6",
    "results": 1,
    "page": 1,
    "version": "1.3"
  }
}

```

To import the JSON data into Google Sheets (or a CSV file), you can use [this workflow](https://app.n8n.io/workflows/1736) that consists of only three nodes.

![workflow](./blog_images/importjson_workflow_jsonfilecsvfile.png)

1. **Read Binary File node** reads the local CSV file.
2. **Move Binary Data node** converts the data from binary to JSON format.
3. a) **Google Sheets node** appends the data to a spreadsheet.
   b) **Spreadsheet File node** writes the data to a CSV file that you can view and download.

![workflow](./blog_images/importjson_workflow_jsonfilesheets.png)

### Workflow to import a JSON file from Gmail into Google Sheets

It's also possible to import data into Google Sheets (or a CSV file) from JSON files sent as attachments via email.

[This workflow](https://app.n8n.io/workflows/1734) does just that using the [**Gmail node**](https://docs.n8n.io/integrations/nodes/n8n-nodes-base.gmail/), which reads the contents of an email, including the attached JSON file. From there, the configuration of the Move Binary Data and Google Sheets nodes is similar to the one in the previous workflows.

![workflow](./blog_images/importjson_workflow_gmailsheets.png)

## What's next?

In this post, you learned how to import JSON into Google Sheets in different ways: using custom code, the App Script, and n8n workflows. Now you have several workflow templates for converting data between JSON and CSV, and importing it into Google Sheets automatically. 

Here's what you can do next:

- Read more tutorials about importing data into Google Sheets, for example [example](https://blog.n8n.io//).
- Check out the [workflow page](https://n8n.io/workflows/) for more automation ideas.
- [Subscribe to our newsletter](https://n8n.io/blog/#subscribe) to get the latest news around workflow automation with n8n.
- Join the [community forum](https://community.n8n.io/) and follow us on [Twitter](https://twitter.com/n8n_io).


> This post was originally published on the [n8n blog](https://blog.n8n.io/google-sheets-import-json/).