Webhooks integration guide
===================================

Webhooks facilitates communication with third-party applications by sending instant web notifications every time an event occurs in Agile CRM. By letting you register a URL that we will notify anytime an event happens in your Agile CRM. When the event occurs—for example, when a successful contact is created , Agile CRM creates an Event object. This object contains all the relevant information about what just happened, including the type of event and the data associated with that event. Agile CRM then sends the Event object to any URLs in your account's webhooks settings via an HTTP POST request. 

 - **Agile CRM web hooks is located at** - Admin Settings > Webhooks
 
![alt text](https://raw.githubusercontent.com/agilecrm/agile-crm-json-io-node/master/Screenshots/jsonio_dialog.png "JSONIO node")

 - **List of Fields in Webhook** 
 
|Field Name|Description|Data Type|
|:-----|:------|:--------------|
|Notify URL|Specify the REST API URL of the third-party application.|URL|
|Module|Contact and Deal|Check Box|
|Trigger Event|Contact is Created,Contact is Updated, Opportunity is Created, Opportunity is Updated|Json Data|


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

- **Step2** -  Enter the address to your webhook endpoint on our admain > webhook page

![alt text](https://raw.githubusercontent.com/agilecrm/agile-crm-json-io-node/master/Screenshots/jsonio_dialog.png "JSONIO node")

- **Step3** -  Click the "Save" button to ensure your endpoint is configured properly.

- **Step4** -  Your endpoint can then return JSON containing the two field eventName and eventData. 
