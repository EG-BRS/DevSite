---
description: Introduction to our REST API.
---

# The Xena API

Xena’s REST based API is documented with Swagger and can be browsed under our API section. To use the API there are a few things you should know, so lets get started on the basics.

### Apikeys or OAuth?

The first thing that should be considered when designing an App for Xena is how authentication should be done. Xena supports two kinds of authentication and they are both usefull in different senarios. Generally speaking the choice can be narrowed down to:

{% hint style="info" %}
Do you want to interact as an user in Xena and/or do you want your app to be cost-free for the user?
{% endhint %}

If the answer to the above question is “yes”, then OAuth is that way to go. If not, then you can use API-keys.



The choice can also be based on the pros and cons of each of the methods:

#### OAuth:

| Pros | Cons |
| :--- | :--- |
| Interact as the enduser, whatever the user can do, the app will be able to do. | Complex implementation compared to API-keys |
| Cross-fiscalsetup actions possible. | Requires App in Xenas Appstore |
| “One click” access for the user, no setup hassle. |  |
| Role based security, your app will have the same role as the user using the app. |  |
| License free \(No additional cost in Xena\) |  |

#### API keys:

| Pros | Cons |
| :--- | :--- |
| Easy implementation compared to OAuth. | The user has to copy/paste API-keys to your app. |
| It is optional to create an app in Xenas appstore | API-keys are licensed as normal user in Xena \(Adds cost to the user\). |
|  | One API-key per fiscalsetup |
|  | No access control. API-key is equal to the administrator role. |

