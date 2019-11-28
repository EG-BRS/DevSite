# Using Meta and Custom data

In Xena apps are able to store two distinct types of data - MetaData and CustomData. MetaData is extra/app-specific data related to a specific entity in Xena. CustomData can be used for almost anything and can act as a kind of small data storage for the app.

Both Meta and Custom data has no predefined structure of the data it stores. What is posted is also what is returned when getting it again. The only requirment is that it is json.

## MetaData

{% hint style="info" %}
For a complete overview of the MetaData methods, please go to [https://xena.biz/api-doc/general/#/Developer - ApiXenaAppMetaData](https://xena.biz/api-doc/general/#/Developer%20-%20ApiXenaAppMetaData)
{% endhint %}

Each app can store its own MetaData related to a specific entity in Xena (fiscalsetup, order, partner, appointment, article, or ledgertag). The MetaData from each app is also indexed so it is searchable. NB: Each app can only store one instance per entity.

{% api-method method="post" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/XenaAppMetaData/{entityType}/{entityId}/{xenaAppId}" %}
{% api-method-summary %}
Insert MetaData
{% endapi-method-summary %}

{% api-method-description %}
Inserts an instance of MetaData. NB: If the instance exists it will be overwritten
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="entityType" type="string" required=true %}
The entity type. Supported entity types: fiscalsetup, order, partner, appointment, article, ledgertag
{% endapi-method-parameter %}
{% api-method-parameter name="entityId" type="long" required=true %}
The entity id
{% endapi-method-parameter %}
{% api-method-parameter name="xenaAppId" type="long" required=true %}
The app id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% api-method-request-example %}
```
{ ...The app-specific json body here... }
```
{% endapi-method-request-example %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}
{% tabs %}
{% tab title="OK" %}
```
{
	"Success" = true, 
	"AssignedId" = "" // {entityType}_{fiscalId}_{entityId}_{xenaAppId}
}
```
{% endtab %}
{% tab title="Error" %}
```
{
	"Success" = false, 
	"Errors" = ["Error1", "Error2"]
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/XenaAppMetaData/{entityType}/{entityId}/{xenaAppId}" %}
{% api-method-summary %}
Update MetaData
{% endapi-method-summary %}

{% api-method-description %}
Updates an instance of MetaData. NB: If the instance does not exist it will be inserted
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="entityType" type="string" required=true %}
The entity type. Supported entity types: fiscalsetup, order, partner, appointment, article, ledgertag
{% endapi-method-parameter %}
{% api-method-parameter name="entityId" type="long" required=true %}
The entity id
{% endapi-method-parameter %}
{% api-method-parameter name="xenaAppId" type="long" required=true %}
The app id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% api-method-request-example %}
```
{ ...The app-specific json body here... }
```
{% endapi-method-request-example %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}
{% tabs %}
{% tab title="OK" %}
```
{
	"Success" = true, 
	"AssignedId" = "" // {entityType}_{fiscalId}_{entityId}_{xenaAppId}
}
```
{% endtab %}
{% tab title="Error" %}
```
{
	"Success" = false, 
	"Errors" = ["Error1", "Error2"]
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/XenaAppMetaData/{entityType}/{entityId}/{xenaAppId}" %}
{% api-method-summary %}
Get MetaData
{% endapi-method-summary %}

{% api-method-description %}
Gets a specific MetaData
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="entityType" type="string" required=true %}
The entity type. Supported entity types: fiscalsetup, order, partner, appointment, article, ledgertag
{% endapi-method-parameter %}
{% api-method-parameter name="entityId" type="long" required=true %}
The entity id
{% endapi-method-parameter %}
{% api-method-parameter name="xenaAppId" type="long" required=true %}
The app id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}
{% tabs %}
{% tab title="OK" %}
```
{ ...The app-specific json body here... }
```
{% endtab %}
{% tab title="Error" %}
```
{
	"Success" = false, 
	"Errors" = ["Error1", "Error2"]
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


## CustomData

{% hint style="info" %}
For a complete overview of the CustomData methods, please go to [https://xena.biz/api-doc/general/#/Developer - ApiXenaCustomData](https://xena.biz/api-doc/general/#/Developer%20-%20ApiXenaCustomData)
{% endhint %}

Each app can store one or more custom data instances of different custom types.

{% api-method method="post" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/Api/Fiscal/{fiscalId}/XenaCustomData/{xenaAppId}/{customType}" %}
{% api-method-summary %}
Insert CustomData
{% endapi-method-summary %}

{% api-method-description %}
Inserts an instance of CustomData
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="xenaAppId" type="long" required=true %}
The app id
{% endapi-method-parameter %}
{% api-method-parameter name="customType" type="string" required=true %}
The app-specific type
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% api-method-request-example %}
```
{ ...The app-specific json body here... }
```
{% endapi-method-request-example %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}
{% tabs %}
{% tab title="OK" %}
```
{
	"Success" = true, 
	"AssignedId" = "" // Guid
}
```
{% endtab %}
{% tab title="Error" %}
```
{
	"Success" = false, 
	"Errors" = ["Error1", "Error2"]
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/Api/Fiscal/{fiscalId}/XenaCustomData/{xenaAppId}/{customType}/{id}" %}
{% api-method-summary %}
Update CustomData
{% endapi-method-summary %}

{% api-method-description %}
Updates an instance of CustomData
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="xenaAppId" type="long" required=true %}
The app id
{% endapi-method-parameter %}
{% api-method-parameter name="customType" type="string" required=true %}
The app-specific type
{% endapi-method-parameter %}
{% api-method-parameter name="id" type="Guid" required=true %}
The instance id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% api-method-request-example %}
```
{ ...The app-specific json body here... }
```
{% endapi-method-request-example %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}
{% tabs %}
{% tab title="OK" %}
```
{
	"Success" = true
}
```
{% endtab %}
{% tab title="Error" %}
```
{
	"Success" = false, 
	"Errors" = ["Error1", "Error2"]
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/Api/Fiscal/{fiscalId}/XenaCustomData/{xenaAppId}/{customType}/{id}" %}
{% api-method-summary %}
Get CustomData
{% endapi-method-summary %}

{% api-method-description %}
Gets a specific CustomData
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="xenaAppId" type="long" required=true %}
The app id
{% endapi-method-parameter %}
{% api-method-parameter name="customType" type="string" required=true %}
The app-specific type
{% endapi-method-parameter %}
{% api-method-parameter name="id" type="Guid" required=true %}
The instance id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}
{% tabs %}
{% tab title="OK" %}
```
{ ...The app-specific json body here... }
```
{% endtab %}
{% tab title="Error" %}
```
{
	"Success" = false, 
	"Errors" = ["Error1", "Error2"]
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://my.xena.biz/Api/Fiscal/{fiscalId}" path="/Api/Fiscal/{fiscalId}/XenaCustomData/{xenaAppId}/{customType}" %}
{% api-method-summary %}
List CustomData
{% endapi-method-summary %}

{% api-method-description %}
Lists CustomDatas
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="xenaAppId" type="long" required=true %}
The app id
{% endapi-method-parameter %}
{% api-method-parameter name="customType" type="string" required=true %}
The app-specific type
{% endapi-method-parameter %}
{% api-method-parameter name="id" type="Guid" required=true %}
The instance id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}
{% tabs %}
{% tab title="OK" %}
```
{
	"Results" = [
		{ ...The app-specific json body here... }, 
		{ ...The app-specific json body here... }
	],
	"Any" = true|false
}
```
{% endtab %}
{% tab title="Error" %}
```
{
	"Success" = false, 
	"Errors" = ["Error1", "Error2"]
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}
