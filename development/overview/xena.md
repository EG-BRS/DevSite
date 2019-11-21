# Xena

{% hint style="info" %}
For a complete overview of the Xena API, please go to [https://xena.biz/api-doc/](https://xena.biz/api-doc/)
{% endhint %}

## How the create a partner ##



## How to create an order and invoice it##

1. Starte by createing a new order:
POST https://my.xena.biz/Api/Fiscal/{fiscalId}/Order
```json
{
	"ContextType": "ContextType_Customer",
	"PartnerId": null,
	"ProjectId": null,
	"OrderNumber": null,
	"CreateTask": true,
	"InternalNote": null
}
```

ContextType: Whether it should be a Sales order (ContextType_Customer) or Purchase order (ContextType_Supplier).
PartnerId: Id of the Customer or Supplier on the order.
ProjectId: Id of the assosiated project. Only relavant for users of the project mdule.
OrderNumber: This should be null. Only set this if you know what you are doing! This can be relavant if the order is born with a number in some other system (Eg. a webshop). 
CreateTask: If true an ordertask will be created.
InternalNote: Just the internal note.

Xena will return this model to you:
https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderDto.cs

You should save the Id. This you will need later.

2. Add a article to the order
First you need to find the ordertask that you want to add the article to. If CreateTask was true when you created the order. Then you need to find the Id of that ordertask else you need to create a new one.

Get the list of order tasks on an order:
GET https://my.xena.biz/Api/Fiscal/{fiscalId}/Order/{orderId}/OrderTask?ForceNoPaging=true&Page=0&PageSize=100&ShowDeactivated=false
You will get a [PagedResultSet](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Helpers/PagedResultSet.cs) with a list of [this model](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderTaskDto.cs) in Entities back.

Create a new orderTask:
POST https://my.xena.biz/Api/Fiscal/98824/OrderTask
```json
{
  "OrderId": {your order id}
}
```
Xena will return this model to you:
https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderLineDto.cs

You should save the Id.

Now you are ready to add an article. In order to do this you will need the id of the article. Here I assume you got an article id.




## How to create an invoice ##



