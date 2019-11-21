# Xena



{% hint style="info" %}
For a complete overview of the Xena API, please go to [https://xena.biz/api-doc/](https://xena.biz/api-doc/)
{% endhint %}

## How the create a partner

## How to create an order and add articles

In this section we will show you how to create an order and add an article to the order.

{% api-method method="post" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/Order" %}
{% api-method-summary %}
Create an order
{% endapi-method-summary %}

{% api-method-description %}
First step is to create a new order.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="InternalNote" type="string" %}
Just the internal note.
{% endapi-method-parameter %}

{% api-method-parameter type="boolean" name="CreateTask" %}
If true an ordertask will be created.
{% endapi-method-parameter %}

{% api-method-parameter name="OrderNumber" type="integer" %}
This should be null. Only set this if you know what you are doing! This can be relavant if the order is born with a number in some other system \(e.g. a webshop\).
{% endapi-method-parameter %}

{% api-method-parameter name="ProjectId" type="integer" %}
Id of the assosiated project. _Only relevant for users of the project module._
{% endapi-method-parameter %}

{% api-method-parameter name="PartnerId" type="integer" %}
Id of the Customer or Supplier on the order.
{% endapi-method-parameter %}

{% api-method-parameter type="string" required=true name="ContextType" %}
Whether it should be a Sales order \(ContextType\_Customer\) or Purchase order \(ContextType\_Supplier\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Xena will return this model to you: https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderDto.cs
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Save the Id - you will need it later.
{% endhint %}

Now you are ready to get the available tasks and add articles to them.

{% api-method method="get" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/Order/{orderId}/OrderTask?ForceNoPaging=true&Page=0&PageSize=100&ShowDeactivated=false" %}
{% api-method-summary %}
Get order tasks
{% endapi-method-summary %}

{% api-method-description %}
First you need to find the ordertask that you want to add the article to. If CreateTask was true when you created the order. Then you need to find the Id of that ordertask else you need to create a new one.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/OrderTask" %}
{% api-method-summary %}
Add an order task
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter type="integer" name="OrderId" required=true %}
Your order task id here
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Xena will return this model to you: https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderLineDto.cs
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
You should save the Id.
{% endhint %}

{% api-method method="post" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/OrderLine" %}
{% api-method-summary %}
Add article to order task
{% endapi-method-summary %}

{% api-method-description %}
Now you are ready to add an article to the ordertask. To do this, you will need the id of the article and to create an ordertaskline. Here I assume you got an article id.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter type="integer" name="OrderTaskId" required=true %}
Your order task id here
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
This will return this model. You should save the data since you will need it when updating the line with the article id.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/OrderLine/{orderlineId}" %}
{% api-method-summary %}
Update a task line
{% endapi-method-summary %}

{% api-method-description %}
To update the line make the following request. The important field are `ArticleId`, `Quantity` and `Description`. See the full model here.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

1. Starte by createing a new order:

   POST [https://my.xena.biz/Api/Fiscal/{fiscalId}/Order](https://my.xena.biz/Api/Fiscal/{fiscalId}/Order)

   ```javascript
   {
    "ContextType": "ContextType_Customer",
    "PartnerId": null,
    "ProjectId": null,
    "OrderNumber": null,
    "CreateTask": true,
    "InternalNote": null
   }
   ```

ContextType: Whether it should be a Sales order \(ContextType\_Customer\) or Purchase order \(ContextType\_Supplier\). PartnerId: Id of the Customer or Supplier on the order. ProjectId: Id of the assosiated project. Only relavant for users of the project mdule. OrderNumber: This should be null. Only set this if you know what you are doing! This can be relavant if the order is born with a number in some other system \(Eg. a webshop\). CreateTask: If true an ordertask will be created. InternalNote: Just the internal note.

Xena will return this model to you: [https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderDto.cs](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderDto.cs)

You should save the Id. This you will need later.

1. Add a article to the order

   First you need to find the ordertask that you want to add the article to. If CreateTask was true when you created the order. Then you need to find the Id of that ordertask else you need to create a new one.

Get the list of order tasks on an order: GET [https://my.xena.biz/Api/Fiscal/{fiscalId}/Order/{orderId}/OrderTask?ForceNoPaging=true&Page=0&PageSize=100&ShowDeactivated=false](https://my.xena.biz/Api/Fiscal/{fiscalId}/Order/{orderId}/OrderTask?ForceNoPaging=true&Page=0&PageSize=100&ShowDeactivated=false) You will get a [PagedResultSet](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Helpers/PagedResultSet.cs) with a list of [this model](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderTaskDto.cs) in Entities back.

Create a new orderTask: POST [https://my.xena.biz/Api/Fiscal/98824/OrderTask](https://my.xena.biz/Api/Fiscal/98824/OrderTask)

```javascript
{
  "OrderId": {your order id}
}
```

Xena will return this model to you: [https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderLineDto.cs](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderLineDto.cs)

You should save the Id.

Now you are ready to add an article to the ordertask. In order to do this you will need the id of the article and to create an ordertaskline. Here I assume you got an article id.

POST [https://my.xena.biz/Api/Fiscal/98824/OrderLine](https://my.xena.biz/Api/Fiscal/98824/OrderLine)

```javascript
{
  "OrderTaskId": {your order task id here}
}
```

This will return [this](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderLineDto.cs) model. You should save the data since you will need it when updating the line with the article id.

To update the line make the following request: PUT [https://my.xena.biz/Api/Fiscal/{fiscalId}/OrderLine/{orderlineId}](https://my.xena.biz/Api/Fiscal/{fiscalId}/OrderLine/{orderlineId})

```javascript
{
  {
    "OrderTaskId": 518296597,
    "Version": 1,
    "IsDeactivated": false,
    "FiscalSetupId": 98824,
    "LocationId": null,
    "OrderInvoiceTaskId": null,
    "OrderId": 518303757,
    "ProjectId": null,
    "Index": 1,
    "ArticleId": 195803359,
    "InvoiceDateDays": null,
    "CostEach": 0,
    "Description": "",
    "PriceEach": 0,
    "Quantity": 0,
    "UnitId": null,
    "PayerId": null,
    "PayerAccountNumber": null,
    "UnitAbbreviation": null,
    "ArticleNumber": null,
    "Totals": {
        "PriceNettTotal": 0,
        "CostTotal": 0,
        "DiscountTotalRatio": 0,
        "DiscountTotalPct": 0,
        "DiscountTotal": 0,
        "MarginTotal": 0,
        "MarginTotalRatio": 0,
        "MarginTotalPct": 0,
        "VatEstTotal": 0
    },
    "ArticleGroupId": null,
    "ArticleVariantId": null,
    "ArticleGroupDescription": null,
    "ArticleHasInventoryManagement": false,
    "ArticleHasVariants": false,
    "ArticleInternalNote": null,
    "ArticleIsBundle": false,
    "ArticleVariantAbbreviation": null,
    "ArticleWeight": null,
    "LocationAbbreviation": null,
    "ArticleStatus": null,
    "OrderDeliveryTransactionId": null,
    "ArticleMappingId": null,
    "ArticleMappingQuantity": null,
    "PartnerArticleNumber": null,
    "IsConfirmed": false,
    "ArticleAbbreviation": "yde1",
    "IsDelivered": false,
    "ArticleIsDeactivated": false,
    "AverageCostPrice": null,
    "EstimatedCostTotal": 0,
    "OrderLineStatusColor": null,
    "OrderLineStatusName": null,
    "HasLinkedLines": false,
    "Id": 518397661
}
}
```

The important field are ArticleId, Quantity, Description and .See the full model [here.](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderLineDto.cs)

## How to create an invoice

