# Xena

{% hint style="info" %}
For a complete overview of the Xena API, please go to [https://xena.biz/api-doc/](https://xena.biz/api-doc/)
{% endhint %}

## How the create a partner

A partner in Xena can be used as a creditor, debtor and/or employee. The idea behind this is to avoid duplicate data and to give our customers a better overview of all of their business with a specific partner. If a partner is a creditor then the partner will have a customer context connected. If a partner is a debtor then the partner will have a supplier context connected. A partner can have more than one context. When you make a lookup on a specific partner. Then you will get info about the contexts associated.

```javascript
GET https://my.xena.biz/Api/Fiscal/{fiscalId}/Partner/{partnerId}
{
	...
	"SupplierId": {Supplier context id},
	"CustomerId": {customer context id},
	"ResourceId": {resource context id},
	...
}
```

This is important to understand when you are creating a new partner. If you use the default endpoint then the partner will be created without any contexts.

{% hint style="info" %}
There are two ways to creating a partner. The first method requires two API calls. The second method can only create a customer or supplier but only requires one API call.
{% endhint %}

{% api-method method="post" host="https://my.xena.biz" path="/Api/Fiscal/{fiscalId}/Partner" %}
{% api-method-summary %}
Create a partner without any context
{% endapi-method-summary %}

{% api-method-description %}
Create a basic partner without any customer or supplier context. See the full dto here:  
https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/PartnerDto.cs
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="FiscalId" type="string" required=false %}
Id of the fiscal you want to create the partner in
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="DefaultDeliveryAddressId" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="Address" type="object" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="ReferenceUserId" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="Attention" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="PartnerType" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="PhoneNumber" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="Note" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="GLNNumber" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="OrgNumber" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="SupplierId" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="CustomerId" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="ResourceId" type="integer" required=false %}

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
	"FiscalSetupId": 97190,
	"CreatedAt": "2019-11-26T10:25:53.307Z",
	"AccountNumber": 10229,
	"Address": {
		"City": "Aarhus",
		"CountryName": null,
		"PlaceName": "string",
		"Street": "string",
		"Zip": "8000",
		"Name": "string",
		"Description": "string - string, 8000 Aarhus",
		"CountryDisplayName": null
	},
	"ReferenceFiscalSetupId": null,
	"ReferenceUserId": null,
	"Attention": "string",
	"PartnerType": "xena_partnertype_company",
	"PartnerTypeTranslated": "Company",
	"PhoneNumber": "string",
	"Note": "string",
	"URL": null,
	"GLNNumber": "string",
	"OrgNumber": "string",
	"SupplierId": null,
	"CustomerId": null,
	"ResourceId": null,
	"DefaultDeliveryAddressId": null,
	"ShortDescription": "10229",
	"LongDescription": "10229 - string",
	"Tags": [],
	"Id": 520618279
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This will create a new partner in Xena. In Xena the partner can be converted to a customer, supplier oo/and employee. If you want to add a context you can use the following endpoint.

{% api-method method="post" host="https://my.xena.biz" path="/Api/Fiscal/{fiscalId}/PartnerContext" %}
{% api-method-summary %}
Create a partner context
{% endapi-method-summary %}

{% api-method-description %}
Create a supplier or customer context for a given partner.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="ContextType" type="string" required=false %}
ContextType\_Customer or ContextType\_Supplier
{% endapi-method-parameter %}

{% api-method-parameter name="PartnerId" type="integer" required=false %}
Id of the partner
{% endapi-method-parameter %}

{% api-method-parameter name="InvoiceEmail" type="string" required=false %}
The email that will be suggested when creating an invoice
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% tabs %}
{% tab title="Supplier context" %}
```
{
	"Version": 1,
	"IsDeactivated": false,
	"FiscalSetupId": 97190,
	"CreatedAt": "2019-11-26T12:52:50.89Z",
	"ContextType": "ContextType_Supplier",
	"PartnerId": 365830428,
	"TermsOfPayment": {
		"Offset": 15,
		"DueType": "xena_running_month",
		"Description": "Running month + 15 days"
	},
	"CurrencyAbbreviation": "DKK",
	"InvoiceEmail": "",
	"OfferReportLayoutId": null,
	"DeliveryReportLayoutId": null,
	"InvoiceReportLayoutId": null,
	"ConfirmationReportLayoutId": null,
	"PriceGroupId": null,
	"Culture": "da-DK",
	"DefaultArticleGroupId": null,
	"DefaultLedgerTagId": null,
	"DefaultVatId": null,
	"DefaultLedgerAccount": null,
	"PaymentMeansType": null,
	"PaymentMeansTypeTranslated": "",
	"Account": null,
	"AccountIdentifier": null,
	"AccountLabelTranslated": "",
	"AccountIdentifierLabelTranslated": "",
	"GroupPayments": false,
	"DefaultPaymentMessage": null,
	"PartnerName": null,
	"DefaultVatAbbreviation": null,
	"PriceGroupDescription": null,
	"ArticleGroupDescription": null,
	"LedgerTagNumber": null,
	"LedgerTagDescription": null,
	"OfferReportLayoutName": null,
	"DeliveryReportLayoutName": null,
	"InvoiceReportLayoutName": null,
	"ConfirmationReportLayoutName": null,
	"CurrencyDescription": "Danish Krone",
	"ContextDescription": "Supplier",
	"CultureDisplayName": "Danish (Denmark)",
	"DefaultBookkeepingText": "",
	"Id": 520693898
}
```
{% endtab %}

{% tab title="Customer context" %}
```
{
	"Version": 1,
	"IsDeactivated": false,
	"FiscalSetupId": 97190,
	"CreatedAt": "2019-11-26T12:54:12.233Z",
	"ContextType": "ContextType_Customer",
	"PartnerId": 516783821,
	"TermsOfPayment": {
		"Offset": 8,
		"DueType": "xena_nett",
		"Description": "Net + 8 days"
	},
	"CurrencyAbbreviation": "DKK",
	"InvoiceEmail": "",
	"OfferReportLayoutId": null,
	"DeliveryReportLayoutId": null,
	"InvoiceReportLayoutId": null,
	"ConfirmationReportLayoutId": null,
	"PriceGroupId": null,
	"Culture": "da-DK",
	"DefaultArticleGroupId": null,
	"DefaultLedgerTagId": null,
	"DefaultVatId": null,
	"DefaultLedgerAccount": null,
	"PaymentMeansType": null,
	"PaymentMeansTypeTranslated": "",
	"Account": null,
	"AccountIdentifier": null,
	"AccountLabelTranslated": "",
	"AccountIdentifierLabelTranslated": "",
	"GroupPayments": false,
	"DefaultPaymentMessage": null,
	"PartnerName": null,
	"DefaultVatAbbreviation": null,
	"PriceGroupDescription": null,
	"ArticleGroupDescription": null,
	"LedgerTagNumber": null,
	"LedgerTagDescription": null,
	"OfferReportLayoutName": null,
	"DeliveryReportLayoutName": null,
	"InvoiceReportLayoutName": null,
	"ConfirmationReportLayoutName": null,
	"CurrencyDescription": "Danish Krone",
	"ContextDescription": "Customer",
	"CultureDisplayName": "Danish (Denmark)",
	"DefaultBookkeepingText": "",
	"Id": 520619084
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}





{% api-method method="post" host="https://my.xena.biz" path="/Api/Fiscal/{fiscal}/Partner/Search" %}
{% api-method-summary %}
Create a partner as a customer and/or supplier
{% endapi-method-summary %}

{% api-method-description %}
To avoid making two requests to xena when creating a customer or supplier this endpoint can be used.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="CustomerTermsOfPaymentOffset" type="integer" required=false %}
Days or months the customer have to pay the invoice
{% endapi-method-parameter %}

{% api-method-parameter name="CustomerTermsOfPaymentDueType" type="string" required=false %}
xena\_cash, xena\_nett, xena\_running\_month or xena\_prepaid
{% endapi-method-parameter %}

{% api-method-parameter name="SupplierTermsOfPaymentOffset" type="integer" required=false %}
Days or months on supplier payment terms
{% endapi-method-parameter %}

{% api-method-parameter name="SupplierTermsOfPaymentDueType" type="string" required=false %}
xena\_cash, xena\_nett, xena\_running\_month or xena\_prepaid
{% endapi-method-parameter %}

{% api-method-parameter name="SendInvite" type="boolean" required=false %}
Leave this as false
{% endapi-method-parameter %}

{% api-method-parameter name="Provider" type="integer" required=false %}
Leave this as null
{% endapi-method-parameter %}

{% api-method-parameter name="ProviderId" type="integer" required=false %}
Leave this as null
{% endapi-method-parameter %}

{% api-method-parameter name="PartnerType" type="string" required=false %}
xena\_partnertype\_person if the partner is a private customer.  
xena\_partnertype\_company if the partner is a company.
{% endapi-method-parameter %}

{% api-method-parameter name="Email" type="string" required=false %}
Customer mail
{% endapi-method-parameter %}

{% api-method-parameter name="Attention" type="string" required=false %}
Partner att
{% endapi-method-parameter %}

{% api-method-parameter name="OrgNumber" type="string" required=false %}
Company registration number \(CVR in DK\)
{% endapi-method-parameter %}

{% api-method-parameter name="GLNNumber" type="string" required=false %}
Number used for electronic invoicing
{% endapi-method-parameter %}

{% api-method-parameter name="Name" type="string" required=false %}
Partner name
{% endapi-method-parameter %}

{% api-method-parameter name="PhoneNumber" type="string" required=false %}
Partner phone number
{% endapi-method-parameter %}

{% api-method-parameter name="Street" type="string" required=false %}
Street
{% endapi-method-parameter %}

{% api-method-parameter name="PlaceName" type="string" required=false %}
Place name
{% endapi-method-parameter %}

{% api-method-parameter name="Zip" type="string" required=false %}
Postal code
{% endapi-method-parameter %}

{% api-method-parameter name="City" type="string" required=false %}
City
{% endapi-method-parameter %}

{% api-method-parameter name="CountryName" type="string" required=false %}
ISO countrycode \(DK, NO, SE etc.\)
{% endapi-method-parameter %}

{% api-method-parameter name="IsCustomer" type="boolean" required=false %}
If this is True then a Customer context will be added to the partner
{% endapi-method-parameter %}

{% api-method-parameter name="IsCupplier" type="boolean" required=false %}
If this is True then a Supplier context will be added to the partner.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
Teh fu
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

The full model can be found here:  
[https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Helpers/PartnerSearchDto.cs](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Helpers/PartnerSearchDto.cs)

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

```text
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
Beskrivelse xxx
{% endapi-method-response-example-description %}

{% tabs %}
{% tab title="OK" %}
```
{
ok json
}
```
{% endtab %}

{% tab title="Error" %}
```
{
error json
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Save the Id - you will need it later.
{% endhint %}

You can find the full model [here](https://github.com/EG-BRS/Xena.Contracts/blob/development/src/Xena.Contracts/Domain/OrderDto.cs)

Articles/lines are add not added directly to the order but to an order task. One order can have seval order tasks. The next step is the get the tasks and add articles to them.

{% api-method method="get" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/Order/{orderId}/OrderTask?ForceNoPaging=true&Page=0&PageSize=100&ShowDeactivated=false" %}
{% api-method-summary %}
Get order tasks
{% endapi-method-summary %}

{% api-method-description %}
First you need to find the ordertask that you want to add the article to. If CreateTask was true when you created the order then the order will have one. To find the Id of that ordertask you need to get the list of order tasks. You will get a PagedResultSet with a list of OrderTaskDTO in Entities property from the endpoint.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="ShowDeactivated" type="boolean" required=false %}
Leave this as false
{% endapi-method-parameter %}

{% api-method-parameter name="Page" type="integer" required=false %}
Page number
{% endapi-method-parameter %}

{% api-method-parameter name="ForceNoPaging" type="boolean" required=false %}
If you set this as True then you will deactivate pageing
{% endapi-method-parameter %}

{% api-method-parameter name="PageSize" type="integer" required=false %}
Page size
{% endapi-method-parameter %}

{% api-method-parameter name="orderId" type="string" required=true %}
Internal order id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text
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



{% api-method method="post" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/OrderTask" %}
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

```text

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
Update an order task line
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

```text
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



## How to create an invoice

