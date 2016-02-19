Webhooks integration guide
===================================

Webhooks facilitates communication with third-party applications by sending instant web notifications every time an event occurs in Agile CRM. Instead of polling to see if data has been updated or created in Agile CRM, you can register a URL to which we will send POSTs containing the updated data and created data. This has benefits for both sides.

[Webhook encyclopedia](https://en.wikipedia.org/wiki/Webhook)

 - **Agile CRM web hooks is located at** - Admin Settings > API & Analytics > Webhooks
 
![alt text](https://raw.githubusercontent.com/agilecrm/webhooks/master/Screenshots/hook2.PNG)

 - **List of Fields in Webhook** 
 
|Field Name|Description|Data Type|
|:-----|:------|:--------------|
|Notify URL|Specify the REST API URL of the third-party application.|URL|
|Module|Contact and Deal|Check Box|



Configuring your webhook settings:
--------

- **Step1** -  Create a webhook endpoint. A webhook endpoint is a URL on your server that will receive each transcript when a event happend, e.g. http://www.example.com/agile_endpoint.php

When trigger event happend, Agile CRM makes HTTP POST to the endpoint you specified. The POST has two data fields, and containing the JSON-encoded transcript.

Here is an example of what a JSON-encoded transcript might look like.

<pre>
{
    "eventName": "Contact is Created",
    "eventData": {
        "cursor": null,
        "count": null,
        "id": 5680673817886720,
        "type": "PERSON",
        "created_time": 1454581629,
        "updated_time": 0,
        "last_contacted": 0,
        "last_emailed": 0,
        "last_campaign_emaild": 0,
        "last_called": 0,
        "viewed_time": 0,
        "viewed": {
            "viewed_time": 0,
            "viewer_id": null
        },
        "star_value": 0,
        "lead_score": 0,
        "tags": [],
        "tagsWithTime": [],
        "properties": [
            {
                "type": "CUSTOM",
                "name": "TeamNumbers",
                "subtype": null,
                "value": "0"
            },
            {
                "type": "SYSTEM",
                "name": "first_name",
                "subtype": null,
                "value": "test"
            },
            {
                "type": "SYSTEM",
                "name": "last_name",
                "subtype": null,
                "value": "hook"
            }
        ]
    }
}
</pre>

- **Step2** -  Enter the address to your webhook endpoint on our Admin Settings > API & Analytics > Webhooks

![alt text](https://raw.githubusercontent.com/agilecrm/webhooks/master/Screenshots/hook3.PNG)

- **Step3** -  Click the "Save" button to ensure your endpoint is configured properly.

- **Step4** -  Your endpoint can then return JSON containing the two field eventName and eventData.

## Sample Data (json formatted)

- **Request Type** -  Contact

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

> Example 3

- **Request Type** -  Deal

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

## Testing Webhooks

The easiest way to test the output of your webhooks is to use a service such as [RequestBin] (http://requestb.in/) or [Postcatcher.in] (http://postcatcher.in/)

These services will give you a URL that will collect requests made to it and let you inspect them in a human-friendly way.
