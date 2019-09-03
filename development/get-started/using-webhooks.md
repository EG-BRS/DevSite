---
description: Essentials on Xena WebHooks.
---

# Using WebHooks

Want to know when a partner’s address changes or when an order is created - Xena Webhooks can be one solution to these situations. Basically you register either for all updates in your fiscal setup of a given type - or listen on a specific id. Whenever something is created/updated or deleted that match your criteria - you get a push notification to the URI, you supplied including which Id and the type of event.

Then you decide whether to fetch the data using either OAuth 2.0 or API-keys to get the actual data that changed. Prime candidates for using Webhooks could be:

* Updating stockcount in a webshop whenever an article is sold or purchased in Xena
* Adding customer to email marketing platform when the customer is created/modified in Xena
* Updating budgetting systems whenever something is bookkept in Xena
* Etc.

## WebHook fundamentals

A webhook consists of three things:

* **Type**  The type of a WebHook defines what type of entity the webhook is triggered on. It could for instance be “Article”, then the webhook is triggered everytime an article is “changed”.
* **Id \(optional\)** The Id of a webhook limits the webhook to only be triggered for a specific entity Id. So if the webhook type is “Article” and the webhook Id is “7”, then the webhook is only triggered when something happens to the article with Id=7. If no Id is specificed on the webhook, it will be triggered on ALL actions on Articles such as creates, modifications and deletions.
* **Callback URI** When the webhook triggeres, this is the URL of the endpoint which is called by Xena with a HTTP POST. Within this HTTP POST is the WebHook Payload, so make sure your endpoint can handle it.

### WebHook payload

A webhook payload consist of three properties and looks something like this:

```javascript
{
 "EntityType": "Article",
 "EntityId": 7,
 "EntityEvent": "Updated"
}
```

The above event means that the article with id 7 has been updated. The entitytype is the same a specified in the webhook itself. The Id is always present\(regardless of what you defined in the webhook\). There are three different events: “Updated”, “Created” and “Deleted”.

### WebHook endpoint response

Every webhook should ALWAYS return a success response with `HTTP200`. The structure of the response should be:

```javascript
{
 "Success": true
}
```

The webhook trigger will be considered “not successful" if the endpoint does not respond within 5 seconds, respond with anything other than `HTTP200` or does not return the JSON data above.

### Activating a webhook

Using webhooks is very easy. They can either be created from the developer section or created via the API \(eg. when an app is activated by the user\). The WebHook API is found on the URL.

## WebHook final thoughts

* Depending on the amount and type of webhooks you create, the webhooks can lead to quite a few requests. Make sure your system can handle the load!
* If your webhook endpoint does not respond within 5 seconds, it will be marked as “failed”.
* If your webhook endpoint does not respond with a `HTTP200` response containing the proper response, the request will be marked as “failed”  .
* If there is more than 10 failed webhook triggers within a 10 minute periode, the webhook will be disabled for 1 hour do prevent Xena from DDOS’ing your system.

