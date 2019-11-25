# Xena



{% hint style="info" %}
For a complete overview of the Xena API, please go to [https://xena.biz/api-doc/](https://xena.biz/api-doc/)
{% endhint %}

## How the create a partner

## How to create an order and add articles

In this section we will show you how to create an order and add an article to that order. This can be done with the following steps:

1. Create the order
2. Finde the ordetask or add an ordertask
3. Add a line to the order
4. Update the orderline the the article

In the following sections we will describe the needed endpoints

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

{% endapi-method-response-example-description %}

```
{
	"Version": 1,
	"IsDeactivated": false,
	"FiscalSetupId": 98824,
	"CreatedAt": "2019-11-21T18:48:14.583Z",
	"PartnerId": null,
	"OurReference": "Niels Husted",
	"YourReference": "",
	"ContextType": "ContextType_Customer",
	"Address": {
		"City": "",
		"CountryName": "DK",
		"PlaceName": "",
		"Street": "",
		"Zip": "",
		"Name": "",
		"Description": " -  ",
		"CountryDisplayName": "Denmark"
	},
	"DeliveryAddress": null,
	"DeliveryNote": null,
	"OrderNumber": 200009,
	"DateDays": 18221,
	"DeliveryDateDays": null,
	"CurrencyAbbreviation": "DKK",
	"OfferReportLayoutId": null,
	"DeliveryReportLayoutId": null,
	"InvoiceReportLayoutId": null,
	"ConfirmationReportLayoutId": null,
	"OfferReportLayoutName": null,
	"DeliveryReportLayoutName": null,
	"InvoiceReportLayoutName": null,
	"ConfirmationReportLayoutName": null,
	"GLNNumber": null,
	"InternalNote": "",
	"TermsOfPayment": {
		"Offset": 8,
		"DueType": "xena_nett",
		"Description": "Net + 8 days"
	},
	"Culture": "da-DK",
	"ProjectId": null,
	"ResponsibleId": 194833467,
	"ResponsibleName": "Niels Husted",
	"InvoiceEmail": "",
	"PartnerAccountNumber": null,
	"PartnerName": null,
	"PartnerNote": null,
	"PartnerPhoneNumber": null,
	"PartnerType": null,
	"Summary": {
		"Totals": {
			"PriceNettTotal": 0.0,
			"CostTotal": 0.0,
			"DiscountTotalRatio": 0.0,
			"DiscountTotalPct": 0.0,
			"DiscountTotal": 0.0,
			"MarginTotal": 0.0,
			"MarginTotalRatio": 0.0,
			"MarginTotalPct": 0.0,
			"VatEstTotal": 0.0
		},
		"NotInvoicedTotals": {
			"PriceNettTotal": 0.0,
			"CostTotal": 0.0,
			"DiscountTotalRatio": 0.0,
			"DiscountTotalPct": 0.0,
			"DiscountTotal": 0.0,
			"MarginTotal": 0.0,
			"MarginTotalRatio": 0.0,
			"MarginTotalPct": 0.0,
			"VatEstTotal": 0.0
		},
		"IsFullyInvoiced": false,
		"IsFullyDelivered": false,
		"IsFullyConfirmed": false,
		"CanOffer": false,
		"CanDeliver": false,
		"CanInvoice": false,
		"CanPay": false,
		"CanConfirm": false
	},
	"OrderInvoiceNumbers": [],
	"DepartmentId": null,
	"DepartmentDescription": null,
	"BearerId": null,
	"BearerDescription": null,
	"PurposeId": null,
	"PurposeDescription": null,
	"IsHeaderReadOnly": false,
	"OrderStatusId": 196093425,
	"OrderStatusName": "Oprettet",
	"OrderStatusColor": "#eac100",
	"ProjectDescription": null,
	"ProjectNumber": null,
	"OrderDeliveryStatus": "SalesOrderDeliveryStatus_NotApplicable",
	"CultureDisplayName": "Danish (Denmark)",
	"LastInvoicedDateDays": null,
	"SupplierInvoiceDateDays": null,
	"SupplierInvoiceNumber": null,
	"SupplierPaymentId": null,
	"Id": 518338659
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}

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

You can find the full DTO here:  
[https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderDto.cs](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderDto.cs)

Articles/lines are add not added directly to the order but to an order task. One order can have seval order tasks. The next step is the get the tasks and add articles to them.

{% api-method method="get" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/Order/{orderId}/OrderTask?ForceNoPaging=true&Page=0&PageSize=100&ShowDeactivated=false" %}
{% api-method-summary %}
Get order tasks
{% endapi-method-summary %}

{% api-method-description %}
First you need to find the order task that you want to add the article to. If CreateTask was true when you created the order then the order will have one. To find the Id of that ordertask you need to get the list of order tasks. You will get a PagedResultSet with a list of this OrderTaskDTO in Entities back.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="orderId" type="string" required=false %}
Internal order id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
	"Count": 1,
	"Entities": [{
		"Version": 1,
		"IsDeactivated": false,
		"FiscalSetupId": 98824,
		"CreatedAt": "2019-11-25T18:37:10.673Z",
		"OrderId": 520562489,
		"OrderContextType": "ContextType_Customer",
		"PrintDetails": false,
		"Details": "",
		"Description": "",
		"OrderTaskStatusId": 196020703,
		"Totals": {
			"PriceNettTotal": 0.0,
			"CostTotal": 0.0,
			"DiscountTotalRatio": 0.0,
			"DiscountTotalPct": 0.0,
			"DiscountTotal": 0.0,
			"MarginTotal": 0.0,
			"MarginTotalRatio": 0.0,
			"MarginTotalPct": 0.0,
			"VatEstTotal": 0.0
		},
		"Address": {
			"City": "",
			"CountryName": "DK",
			"PlaceName": "",
			"Street": "",
			"Zip": "",
			"Name": "",
			"Description": " -  ",
			"CountryDisplayName": "Denmark"
		},
		"DeliveryAddress": null,
		"OrderTaskStatusName": "Igangværende",
		"OrderTaskStatusColor": "#9cce6f",
		"OrderNumber": 200015,
		"Index": 1,
		"SubscriptionId": null,
		"IsInvoiced": false,
		"IsDelivered": false,
		"IsConfirmed": false,
		"IsReadonly": false,
		"Abbreviation": "200015-1",
		"ProjectId": null,
		"ProjectClosedDateDays": null,
		"AppointmentCount": 0,
		"IsPlanned": false,
		"Id": 520556331
	}]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/OrderTask" %}
{% api-method-summary %}
Find an order task
{% endapi-method-summary %}

{% api-method-description %}
If there are no ordertasks on the order or you want to create a new one. Then you can use this endpoint.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter type="integer" name="OrderId" required=true %}
Id for the order you want to create an ordertask on
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Xena will return this model to you: 
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
Create an order task line
{% endapi-method-summary %}

{% api-method-description %}
Now you are ready to add an article to the order task. To do this, you will need the id of the article and to create an ordertaskline. Here I assume you got an article id. Start by creating a new order task line.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="OrderId" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
You should save the data since you will need it when updating the line with the article id.
{% endapi-method-response-example-description %}

```
{
	"Version": 1,
	"IsDeactivated": false,
	"FiscalSetupId": 98824,
	"CreatedAt": "2019-11-25T19:05:54.163Z",
	"OrderId": 520562489,
	"OrderContextType": "ContextType_Customer",
	"PrintDetails": false,
	"Details": "",
	"Description": "",
	"OrderTaskStatusId": 196020703,
	"Totals": {
		"PriceNettTotal": 0.0,
		"CostTotal": 0.0,
		"DiscountTotalRatio": 0.0,
		"DiscountTotalPct": 0.0,
		"DiscountTotal": 0.0,
		"MarginTotal": 0.0,
		"MarginTotalRatio": 0.0,
		"MarginTotalPct": 0.0,
		"VatEstTotal": 0.0
	},
	"Address": {
		"City": "",
		"CountryName": "DK",
		"PlaceName": "",
		"Street": "",
		"Zip": "",
		"Name": "",
		"Description": " -  ",
		"CountryDisplayName": "Denmark"
	},
	"DeliveryAddress": null,
	"OrderTaskStatusName": "Igangværende",
	"OrderTaskStatusColor": "#9cce6f",
	"OrderNumber": 200015,
	"Index": 2,
	"SubscriptionId": null,
	"IsInvoiced": false,
	"IsDelivered": false,
	"IsConfirmed": false,
	"IsReadonly": false,
	"Abbreviation": "200015-2",
	"ProjectId": null,
	"ProjectClosedDateDays": null,
	"AppointmentCount": 0,
	"IsPlanned": false,
	"Id": 520556332
}
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
To update the line make the this request. The important field are `ArticleId`, `Quantity` and `Description`. See the full model here.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="orderlineId" type="integer" required=false %}
Id of the line order you want to update
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
	"Version": 2,
	"IsDeactivated": false,
	"FiscalSetupId": 98824,
	"CreatedAt": "2019-11-25T19:18:42.527Z",
	"LocationId": null,
	"OrderInvoiceTaskId": null,
	"OrderTaskId": 520556332,
	"OrderId": 520562489,
	"ProjectId": null,
	"Index": 0,
	"ArticleId": 195803359,
	"InvoiceDateDays": null,
	"CostEach": 0.00000,
	"Description": "Ydelser sats 1",
	"PriceEach": 0.00000,
	"Quantity": 1.00000,
	"UnitId": 195796629,
	"PayerId": null,
	"PayerAccountNumber": null,
	"UnitAbbreviation": "timer",
	"ArticleNumber": "yde1",
	"Totals": {
		"PriceNettTotal": 0.00000,
		"CostTotal": 0.00000,
		"DiscountTotalRatio": 0.0,
		"DiscountTotalPct": 0.0,
		"DiscountTotal": 0.00000,
		"MarginTotal": 0.00000,
		"MarginTotalRatio": 0.0,
		"MarginTotalPct": 0.0,
		"VatEstTotal": 0.00000
	},
	"ArticleGroupId": 195796691,
	"ArticleVariantId": null,
	"ArticleGroupDescription": "Ydelser",
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
	"EstimatedCostTotal": 0.00000,
	"OrderLineStatusColor": null,
	"OrderLineStatusName": null,
	"HasLinkedLines": false,
	"Id": 520557490
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



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

