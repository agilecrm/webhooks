Agile CRM webhooks
=====================

Agile CRM is a new breed CRM software with sales and marketing automation. You can sign up @ [AgileCRM.com](https://www.agilecrm.com/).  

Table of contents
--------

- [Webhooks integration guide](#webhooks-integration-guide)
- [Configuring your webhooks settings](#configuring-your-webhooks-settings)
- [Sample data (json formatted)](#sample-data-json-formatted)
- [Testing webhooks](#testing-webhooks)

Webhooks integration guide
--------

Webhooks facilitates communication with third-party applications by sending instant web notifications every time an event occurs in Agile CRM by letting you register a URL that we will notify anytime an event happens in your Agile CRM. When the event occurs.

[Webhooks encyclopedia](https://en.wikipedia.org/wiki/Webhook)

 - **Agile CRM web hooks is located at** - Admin Settings > API & Analytics > Webhooks
 
![alt text](https://raw.githubusercontent.com/agilecrm/webhooks/master/Screenshots/hooks5.PNG)

 - **List of fields in webhooks** 
 
|Field name|Description|Data type|
|:-----|:------|:--------------|
|Notify URL|Specify the REST api URL of the third-party application.|URL|
|Module|Contact and Deal|Check box|



Configuring your webhooks settings:
--------

- **Step 1** -  Create a webhooks endpoint. A webhook endpoint is a URL on your server that will receive each transcript when a event happend, e.g. http://www.example.com/agile_endpoint.php

When trigger event happend, Agile CRM makes HTTP POST to the endpoint you specified. The POST has two data fields, and containing the JSON-encoded transcript.

- **Step 2** -  Enter the address to your webhooks endpoint on our Admin Settings > API & Analytics > Webhooks

![alt text](https://raw.githubusercontent.com/agilecrm/webhooks/master/Screenshots/hooks5.PNG)

- **Step 3** -  Click the "Save" button to ensure your endpoint is configured properly.

- **Step 4** -  Your endpoint can then return JSON containing the two field eventName and eventData.

Sample data (json formatted)
--------

- **Request type** -  Contact

> Example 1

<pre>
{
    "eventName": "Contact is Created",
    "eventData": {
        "id": 5667649732214784,
        "type": "PERSON",
        "created_time": 1455855737,
        "properties": [
            {
                "type": "SYSTEM",
                "name": "first_name",
                "subtype": null,
                "value": "John"
            },
            {
                "type": "SYSTEM",
                "name": "last_name",
                "subtype": null,
                "value": "Delta"
            },
            {
                "type": "SYSTEM",
                "name": "email",
                "subtype": "",
                "value": "john@alien.comm  "
            }
        ]
    }
}
</pre>

> Example 2

<pre>
{
    "eventName": "Contact is Updated",
    "eventData": {
        "id": 5667649732214784,
        "type": "PERSON",
        "created_time": 1455855737,
        "updated_time": 1455856605,
        "properties": [
            {
                "type": "SYSTEM",
                "name": "last_name",
                "subtype": null,
                "value": "Delta Updated"
            },
            {
                "type": "SYSTEM",
                "name": "email",
                "subtype": "",
                "value": "john@alien.comm  "
            }
        ]
    }
}
</pre>

- **Request type** -  Deal

> Example 3

<pre>
{
    "eventName": "Opportunity is Created",
    "eventData": {
        "colorName": "GREY",
        "id": 5721670354468864,
        "name": "deal plane",
        "contact_ids": [
            "5667649732214784"
        ],
        "expected_value": 50000,
        "milestone": "Proposal",
        "probability": 95,
        "close_date": null,
        "owner_id": "6263975862861824",
        "pipeline_id": 5730082031140864
    }
}
</pre>

> Example 4

<pre>
{
    "eventName": "Opportunity is Updated",
    "eventData": {
        "colorName": "GREY",
        "id": 5721670354468864,
        "name": "deal plane",
        "contact_ids": [
            "5667649732214784"
        ],
        "expected_value": 50000,
        "milestone": "Proposal",
        "probability": 99,
        "close_date": null,
        "owner_id": "6263975862861824",
        "pipeline_id": 5730082031140864
    }
}
</pre>

Testing webhooks
--------

The easiest way to test the output of your webhooks is to use a service such as [RequestBin] (http://requestb.in/) or [Postcatcher.in] (http://postcatcher.in/)

These services will give you a URL that will collect requests made to it and let you inspect them in a human-friendly way.
